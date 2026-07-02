
## The Core Distinction:

* Inheritance models "is-a" - `Sphere` is a `Shape`
* Composition models "has-a" - `Space ship` has a `Transform`, has a `Mesh`, has a  `Velocity`
  
```cpp
// Inheritance: Player IS-A Entity
class Player : public Entity {/* ... */};

// Composition: Player HAS-A Transform, HAS-A Mesh
class Player {
	Transform transform;
	Mesh mesh;
};
```

## Full Comparison Table:

| Aspect                 | Inheritance                                            | Composition                                  |
| :--------------------- | ------------------------------------------------------ | -------------------------------------------- |
| Relationship           | "is-a"                                                 | "has-a" / "uses-a"                           |
| Coupling               | Tight-child knows base's internals (protected members) | Loose-only public inheritance used           |
| Flexibility at runtime | Fixed at compile time (mostly)                         | Can swap parts at runtime                    |
| Code reuse             | Reuses behavior by extension                           | Reuses behavior by delegation                |
| Polymorphism           | Built-in via virtual functions                         | Requires explicit interfaces                 |
| Memory layout          | Single contiguous block (base + derived)               | Parts may live anywhere (depends on storage) |
| Multiple parents       | Multiple inheritance (messy diamond problem)           | Trivial - just add more members              |
| Encapsulation          | Base's protected exposed to children                   | Owner only sees public inheritance           |
| Testability            | Harder-must mock entire base                           | Easier-swap a component                      |
| Common pifall          | Deep hierarchies become rigid                          | Can lead to wordy delegation                 |

## A Concrete Example: A 3D Object:

```cpp
class GameObject {
protected:
	Vector3 position;
	Vector3 rotation;
	
public:
	virtual void update(float dt) = 0;
	virtual void draw() const = 0;
	virtual ~GameObject() {}
};

class Sphere : public GameObject {
	float radius;
	Color color;
	
public:
	Sphere(Vector3 pos, float r, Color c) : radius(r), color(c) {
		position = pos;
	}
	
	void update(float dt) override { /* spin, bounce, etc. */ }
	void draw() const override { DrawSphere(position, radius, color); }
};

class Cube : public GameObject {
	Vector3 size;
	Color color;

public:
	void update(float dt) override { /* */ }
	void draw() const override {
		DrawCube(position, size.x, size.y, size.z, color);
	}
};
```

This works fine for small projects. The problem appears when you want a Sphere that also has physics, AI, a particle trail and networking...

You end up with deep, brittle hierarchy or with ***multiple inheritance*** that fights you.

## The Composition Approach:

```cpp
struct Transform {
	Vector3 position {0, 0, 0};
	Vector3 rotation {0, 0, 0};
	Vector3 scale {1, 1, 1};
};

struct Velocity {
	Vector3 linear {0, 0, 0};
	Vector3 angular {0, 0, 0};
};

struct SphereRenderer {
	float radius;
	Color color;
	
	void draw(const Transform& t) const {
		DrawSphere(t.position, radius, color);
	}
};

class Ball {
	Transform transform;
	Velocity velocity;
	SphereRenderer renderer;
	
public:
	Ball(Vector3 pos, float r, Color c) : transform{pos}, renderer{r, c} {}
	
	void update(float dt) {
		transform.position.x = velocity.linear.x * dt;
		transform.position.y = velocity.linear.y * dt;
		transform.position.z = velocity.linear.z * dt;
	}
	
	void draw() const { renderer.draw(transform); }
	
	Transform& getTransform() { return transform; }
	Velocity& getVelocity() { return velocity; }
};
```

Now `Transform`, `Velocity` and `SphereRenderer` are ***independent***, ***reusable*** pieces

Any object can pick the pieces it needs. This is essentially what game engines call the ***Entry-Component pattern*** - and it's why most modern engines (Unity, Unreal, Bevy) favor composition.

## When to Pick Which (Practical Rules):

### Use inheritance when:

* There's a true "is-a" relationship that won't shift.
* You need ***runtime polymorphism through a clean interface*** (abstract base + many implementations). This is inheritance's strongest case.
* The interface is small and stable.

### Use composition when:

* You're combining unrelated capabilities a thing that renders AND collides AND moves).
* You want to swap behavior at runtime.
* You're building anything resembling a game engine - entities are best made of parts.

### A useful guideline:

If you find yourself adding a virtual method, just to delegate to a member you would have added anyway, you probably wanted composition.

## Pointers, References, and Ownership:

In C++, how you store the parts matters as much as which model you choose. Here are the main options:

### 1. By Value (the default - prefer this):

```cpp
class Ball {
	Transform transform;    // owned, stored inline, no allocation
	Velocity velocity;
}
```

Cache-friendly no allocation, no null checks. Use this unless you have a reason not to.

### 2. Raw Pointers - Non-Owning References:

A raw pointer (``T*``) should mean ***"I'm looking at this, I don't own it."***
Useful when several objects need to reference the same external thing.

```cpp
class Bullet {
	Transform transform;
	const Player* shooter;

public:
	Bullet(const Player* p) : shooter(p) {}
};
```

Key rule: ***a raw pointer must never delete***. If your code does, switch to a smart pointer.

### 3. `std::unique_ptr<T>` - Single Ownership:

Use this when one object owns another and you need ***polymorphism*** or ***heap allocation***.
It automatically deletes when it goes out of scope.

```cpp
#include <memory>
#include <vector>

class Shape {
public:
	virtual void draw() const = 0;
	virtual ~Shape() = default;
};

class Sphere : public Shape {/* ... */};
class Cube : public Shape {/* ... */};

class Scene {
	std::vector<std::unique_ptr<Shape>> shapes;
public:
	void add(std::unique_ptr<Shape> s) {
		shape.push_back(std::move(s));    // transfer ownership
	}
	void drawAll() const {
		for (const auto& s: shapes) s -> draw();
	}
};

// Usage:

Scene scene;
scene.add(std::make_unique<Sphere>(/* ... */));
scene.add(std::make_unique<Cube>(/* ... */));

// Mo manual delete; cleanup is automatic
```

This is canonical pattern for a heterogeneous collection of polymorphic objects.

### 4. `std::shared_ptr<T>` - Shared Ownership:

Use only when ***multiple owners genuinely need to keep the object alive***

It uses a reference count, so it's heavier than `unique_ptr`. In simulation/game code it's often overused - most "I need to reference this" cases want a raw pointer or an ID/index instead.

```cpp
auto mesh = std::make_shared<Mesh>(/* heavy data */);

ObjectA a(mesh);    // both A and B point at the same mesh.
ObjectB b(mesh);

// Mesh is destroyed only when both A and B are gone.
```

### 5. References(T&) - Borrowed, Non-Owning, Never Null:

Best for function parameters where you guarantee something exists:

```cpp
void applyGravity(Velocity& v, float dt) {
	v.linear.y -= 9.81f * dt;
}
```

References ***can't be reseated*** and ***can't be null*** - exactly when you want for "borrow this for the duration of the call.".

## Three Pointer Patterns for your Raylib Simulation:

### Pattern A: Polymorphic Scene Graph (composition + inheritance combined).

The sweet spot is often ***composition for the data***, ***inheritance for the interface***.

A ***Renderable***  interface allows you mixed object types in one container:

```cpp
class Renderable {
public:
	
	virtual void draw() const = 0;
	virtual ~Renderable() = default;
};

class Ball : public Renderable {
	Transform transform;
	Velocity velocity;
	SphereRenderer renderer;
	
public:
	void draw() const override { renderer.draw(transform); }
	void update(float dt) {/* ... */}
};

class Scene {
	std::vector<std::unique_ptr<Renderable>> object;

public:
	void draw() const {
		for (const auto& obj : objects) obj->daraw();
	}
};
```

### Pattern B: Parent-child via Non-Owning Pointers:

For hierarchical transforms (a turret on top of a rank), children often need to know their parent-but they don't own it.

```cpp
class SceneNode {
	Transform local;
	SceneNode* parent = nullptr;
	std::vector<std::unique_ptr<SceneNode>>
}
```