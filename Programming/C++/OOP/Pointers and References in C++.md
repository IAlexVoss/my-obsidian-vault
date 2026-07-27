Pointers and references are two ways in C++ lets you work with an object ***indirectly*** - through its address instead of through a copy.

In everyday application code you can avoid them, but in ***games***, ***simulations*** and ***engines*** they are unavoidable: you use them to ***control memory***, ***avoid copy large objects every frame***, ***share state between systems***, and get runtime polymorphism for entry hierarchies.

This note builds up from the memory model, then covers ***pointers***, ***references***, ***const***, ***function params***, ***dynamic memory***, ***smart pointers***, ***polymorphism***, and finally concrete game/simulation patterns and pitfalls.

# Why this matters for games and simulations:

**No hidden copies in the loop**: A simulation updates thousands of objects per time

Passing a big `Transform` or `Mesh` by value copies it every call. Passing by reference or pointer passes only an address (usually 8 bytes).

**Shared state between systems**: The physics system, the renderer, and the AI all need to look at the same entity, not private copies. Indirection lets many systems see one object.

**Runtime polymorphism**: `Enemy`, `Player`, `Projectile` all derive from `Entity`. To call the right `update()` at runtime you must go through a base-class pointer or reference.

**Explicit ownership and lifetime**: Engines create and destroy objects constantly. Pointers (especially smart pointers) let you express ***who owns what and when it dies***.

# Memory model: stack VS heap:

Every object ***lives at some address in memory***. There are two regions you care about:

**Stack** - automatic storage. Local variables live here. Fast, freed automatically when the scope ends. Limited in size.
**Heap** - (free storage) - dynamic storage. You request memory explicitly and it says alive until you release it.

Larger, but slower to allocate and your responsibility to free.

```cpp
void example() {
	int a = 10;               // 'a' lives on the stack, freed at end of function
	int* p = new int(20);     // the int lives on the heap; 'p' (on the stack) holds its adderess
	delete p;                 // you must free heap memory manually, or use a smart pointer.
}
```

A pointer or reference is just a way to name an address so you can reach the object living there.

# Pointers:

A ***pointer*** is a variable whose value is the memory address of another object.

## Declaring and using a pointer:

Three operations matter:

`*` - in a declaration means "pointer to";
`&` - (address-of) gives you the address of an object;
`*` - (dereference) gives you the object a pointer points to.

```cpp
int hp = 100;
int* p = &hp;    // p holds the address of hp
// "p" is a pointer to int, initiaized with the address of hp

std::cout << p;  // prints an address, e.g. 0x7ffc...
std::cout << *p; // prints 100 -> dereference the value AT that address

*p = 75;         // writes through the pointer; now hp == 75
std::cout << hp; // prints 75
```

Read `*p` as "the thing p points to". Writing to `*p` modifiers the original object, because the pointer refers to the same memory.

## `nullptr` - a pointer to nothing:

A pointer that doesn't point at a void object should be `nullptr` (modern C++ prefer it over the `NULL` or `0`).

```cpp
int* target = nullptr;    // points to nothing yet
if (target != nullptr) {
	// always check before dereferencting
	attack(*target);
}
// shorthabd: if (target) {...}
```

Dereferencing a `nullptr` (`*target` when `target == nullptr`) is ***undefined behavior*** - usually a crash. Checking for null is how you model "optional" links e.g. `Entity* currentTarget` that may or may not exist.

## Reading pointer declarations:

The `*` binds to the variable, not the type. This surprises people:

```cpp
int* a, b;  // a is int* but b is a plain int
int *a, *b; // both pointers - clearer to write if this way
```

## Pointer to Pointer:

A pointer can point to another pointer. You rarely need this in game logic, but you'll see it in C-style APIs and 2D arrays.

```cpp
int x = 5;
int* p = &x;
int** pp = &p;        // pp points to p. which points to x
std::cout << **pp;    // prints 5 (dereference twice)
```

# References:

A `reference` is an ***alias*** - another name for an existing object.
Once bound, the reference is that object for all practical purposes.

```cpp
int score = 50;
int& ref = score;     // ref is now another name for score.
ref = 80;             // modifiers score through reference
std::cout << score;   // prints 80
```

Two hard rules distinguish references from pointers:

1. A ***reference must be initialized when declared***. There is no "null reference" and no uninitialized reference.
2. ***A reference can never be reseated***. After declaring and initializing.

`int& ref = score`, ref refers to `score` for is entire life.

Assigning to `ref` changes `score`; it does not wake `ref` point elsewhere:

```cpp
int a = 1, b = 2;
int& r = a;
r = b;             // this does NOT rebind r to b. It copies b's value into a. Now a == 2, and r still aliases a
```

Because a reference has no "empty" state and can't be reached, it's the safer, simpler choice when you always have exactly one valid object to refer to - most commonly as a function parameter.

# Pointers VS References - when to use which:

| Feature                            | Pointer `*T`                                                          | Reference `T&`                                                 |
| :--------------------------------- | --------------------------------------------------------------------- | -------------------------------------------------------------- |
| Can be null / "no object"          | Yes (`nullptr`)                                                       | No, must bind to something                                     |
| Can be reseated to another object? | Yes                                                                   | No, bound for life                                             |
| Must be initialized                | No (but you should)                                                   | Yes                                                            |
| Syntax to access value             | `*p`, `p -> member`                                                   | `r`, `r.member` (like a normal variable)                       |
| Pointer ariphmetic                 | Yes                                                                   | No                                                             |
| Typical size                       | Optional / rebindable links ownership, arrays, polymorphic containers | Function parameters, return values. aliases that always exist. |

## Rule of thumb:

Use a ***reference*** when the thing always exists and newer changes identity; Use a ***pointer*** when it can be absent (`nullptr`) or when you need to point it at different objects over time.

# Const correctness:

`const` restricts what you can do through a pointer or reference.

This matters enormously in engine APIs : it leеs you pass a big object cheapy (by address) while ***guaranteeing the function won't modify it***.

## `const` with pointers:

Read this right-to-left:

```cpp
int value = 10;
const int* p1 = &value;    // pointer to const int, can't modify *p1, Can reseat p1
// *p1 = 5;                // Error
p1 = nullptr;              // OK

int* const p2 = &value;    // const pointer to int, can modify *p2, can't reseat p2
*p2 = 5;                   // OK
// p2 = nullptr;           // Error

const int* const p3 = &value;    // const pointer to const int, neither allowed
```

## `const` references - the workhorse:

A ***reference to const*** can read the object but not modify it.
This is the standard way to pass large read-only objects:

```cpp
// Passes only an address, promises not to modify the mesh
float computeVolume(const Mesh& mesh) {
	// mesh.vertices[0] = ...;    // Error: can't modify through const&
	return mesh.boundindgBox().volume();
}
```

A const reference can also bind a ***temporary*** (an r value) and extend its lifetime, which a non-const reference cannot:

```cpp
const int& r = 5;    // OK, binds to a temporary
// int& bad = 5;
```

# Passing objects to functions (the most practical part):

This is where the choice between value, pointer, and reference has the biggest day-to-day impact in a simulation.

## Pass by value - makes a copy:

```cpp
void tick(GameObject state) { ... } // copies the entrie GameState every call
```

Fine for small, cheap types (`int`, `float`, a 2 float vector).

Wasteful for anything large or containing heap data (`vectors`, `strings`, `meshes`).

## Pass by reference - no copy, can modify:

```cpp
void applyDamage(Entity& e, int amount) {
	e.hp -= amount;    // modifiers the caller's object directly
}

Entity boss;
applyDamage(boss, 10); // boss is changed
```

Use this for ***output parameters*** and for ***in-place mutation*** of large objects

## Pass by const reference - no copy, read only:

```cpp
float distance(const Vector3D& a, const Vector3& b) {
	return (a-b).length();    // reads both, copies neither, modifiers neither
}
```

This is the default, you should reach for when a function only needs to read a non-edit object.

## Pass by pointer - no copy, optional, explicit at call site:

```cpp
// nullptr means "no target at this frame"
void aimAt(Turret& t, const Entity* target) {
	if (target) t.rotateTowards(target->position);
}

aimAt(turret, nullptr);        // explicity "no target"
aimAt(turret, &someEnemy);     // the & at the call site signals "might be modified optional"
```

## Guideline:

| You need to...                              | Use           |
| :------------------------------------------ | ------------- |
| Read a small, cheap value                   | pass by value |
| Read a large object without copying         | `const T&`    |
| Modify the caller's object                  | `T&`          |
| Modify it, or accept "no object" (nullable) | `T*`          |

# Pointers and arrays:

Arrays and pointers are closely related: an array name decays to a pointer to its first element, and indexing is defined in terms of pointer arithmetic.

```cpp
int particlesp[4] = {10, 20, 30, 40};
int* p = particles;    // points to particles[0]

*(p + 2);              // == particcles[2] == 30
p[2]                   // identical synax, also 30

++p;                   // now points to particles[1]
                       // pointer arithmetic advances by sizeof(int), not by 1 byte
```

`*(arr  +i)` and `arr[i]` are exactly the same thing. This is why iterating a contiguous storage (like `std::vector`) is fast: the elements it's next to each other in memory and the CPU cache loses that (more on this below).

# Dynamic allocation with `new` / `delete`:

`new` allocates on the heap and returns a pointer;

`delete` frees it. `new[]` / `delete[]` do the same for arrays.

```cpp
Enemy* e = new Enemy();    // heap allocated, lives untill you delete it.

e -> tekeTurn();
delete e;                  // free it - Required, or you leak memory.

int* buffer = new int[100];  // array form
delete[] buffer;             // must use delete[], not just simple delete
```

Raw `new` / `delete` is ***error-prone and discouraged in modern C++***.

Three classic bugs:

	- Memory leak - you forget to delete, memory is never reclaimed. In a game loop this grows every frame untill you run out.
	- Dangling-pointer - you delete but keep using the pointer (use-after-free). Undefined behavior
	- Double free - you delete the same pointer twice. Undefined behavior / crash.

```cpp
Enemy* e = new Enemy();
delete e;
e -> takeTurn();     // BUG: use-after-delete, e is dangling
delete e;            // BUG: double delete
```

The modern answer to all three is ***smart pointers***, which free automatically.

# Smart pointers (modern C++):

Smart pointers wrap a raw pointer and tie its lifetime to an object, so memory is freed automatically when it's no longer needed.

This is RAII (Resource Acquisition Is Initialization): the resource is released by a destructor, deterministically, with no garbage collector.

```cpp
include <memory>
```

## `unique_ptr` - single owner:

`std::unique_ptr<T>` owns its object exclusively. When the `unique_ptr` is destroyed, the object is deleted. It cannot be copied (that would mean two owners), only ***move***.

```cpp
#include <memory>

std::unique_ptr<Enemy> e = std::make_unique<Enemy>();
e -> takeTurn();
// no delete needed-freed automatically when e goes out of scope.
// auto ec = e;      // Error can't copy a unique_ptr

auto ec = std::move(e);   // OK - transfer ownership; e is now empty (nullptr).
```

Use `unique_ptr` as your ***default*** for heap ownership - it has zero overhead compared to a raw pointer and makes ownership unambiguous.

## `shared_ptr` - shared ownership:

`std::shared_ptr<T>` allows multiple owners. It keeps a ***reference count***; the object is deleted when the last `shared_ptr` to it goes away.

```cpp
auto texture = std::make_shared<Texture>("grass.png");
auto copy = texture;    // OK: both shared ownership, ref count == 2
// object is destroyed only when both copy and texture are gone.
```

Useful for shared resources (a texture used by many sprites). It's heavier then `unique_ptr` (the count must be maintained, automatically if threads are involved), so don't reach it by default.

## `weak_ptr` - non owning observer:

`std::weak_ptr<T>` observes an object managed by a `shared_ptr` ***without*** keeping it alive.

You call `.lock()` to temporary get a `shared_ptr` if the object still exists.

Its main job is ***breaking reference cycles*** (see the circular-reference pitfall below).

```cpp
std::shared_ptr<Enemy> e = std::make_shared<Entity>();
std::weak_ptr<Entity> observer = e;    // does not increase the owning count

if (auto locked = observer.lock()) { // is it still alive? 
	locked -> update();
} else {
	// the entity has already been destroyed
}
```

# Ownership summary:

| Type            | Owns?              | Copyable?         | Use for                                    |
| :-------------- | ------------------ | ----------------- | ------------------------------------------ |
| `T*`(raw)       | No (by convention) | Yes               | Non-owning links, "Just looking"           |
| `unique_ptr<T>` | Yes, sole          | No (move-only)    | Default heap ownership                     |
| `shared_ptr<T>` | Yes, shared        | Yes (ref-counted) | Genuinely shared resources                 |
| `weak_ptr<T>`   | No                 | Yes               | Observing a shared object, breaking cycles |

## Modern convention:

owning pointers are smart pointers; a raw pointer means "I'm looking at this but I don't own it, and it's not my job to delete it".

# Pointers, references, and polymorphism:

Runtime polymorphism - calling the right overridden function for the actual object type - only works ***through pointer*** or ***reference to a base class***.

A base-class value can't do it.

```cpp
struct Entity {
	virtual void update() = 0;    // virtual => resolved at runtime
	virtual ~Entity() = default;  // virtual destructor: essential part (see below)
};

struct Enemy : Entity { void update() override { /* chase player */ }};
struct Player : Entity { void update() override { /* read input */ }};

void tick(Entity& e) { // reference to base
	e.update();        // calls Enemy::update or Player::update, correctly
}

Enemy goblin;
tick(goblin);          // runs Enemy::update
```

## Object slicing - a value-semantic trap:

If you copy a derived object into a base class, the derived part is "sliced off":

```cpp
Enemy goblin;
Entity base = goblin;    // BUG: only the Entity part is copied;
                         // the enemy-ness is lost.
//base.update();         // would call the base version, not Enemy's.
```

This is a key reason engines store polymorphic objects as pointers / references, never as base-class values.

## Virtual destructor:

When you delete a derived object through a base pointer, the base destructor ***must be*** `virtual`, or the derived destructor won't run (leak / undefined behavior):

```cpp
Entity* e = new Enemy();
delete e;     // only safe because ~Entity() is virtual.
```

# Patterns in games and simulations:

These combine everything above into the shapes you'll actually write

## Owning a collection of entities:

The world owns its entities; a container of `unique_ptr` gives clear ownership and correct polymorphic destruction:

```cpp
std::vector<std::unique_ptr<Entity>> entities;
entities.push_back(std::make_unique<Enemy>());
entities.push_back(std::make_unique<Player>());

for (const auto& e : entities) e->update();
// polymorphic dispatch, no copies
// all entities are freed automatically when the vector is destroyed.
```

## Non-owning links between systems:

A component often needs to reach back to its entry, or an AI needs a target - but it ***does not*** own it.

Use a raw pointer (nullable) or a reference (always present):

```cpp
struct AIComponent {
	Enity* self = nullptr;    // who I belong to (set once, non-owning)
	Entity* target = nullptr; // may be null: I might have no target.
}
```

The raw pointer here is the correct, idiomatic chooise: it signals "observing it, not owning".

## Scene graph: (parent / child):

The parent owns its children, each child points back to its parent with a ***raw*** pointer.

Using an owning pointer both ways would create a cycle that never frees:

```cpp
struct Node {
	Node* parent = nullptr;    // non-owning, avoids a cycle
	std::vector<std_unique_ptr<Node>> children; // owning
}
```

## Object pool (avoid allocation in the loop):

Calling `new` / `delete` every frame causes fragmentation and stutter.

A pool pre-allocates objects once and hangs out pointers to reuse them:

```cpp
class BulletPool {
	std::vector<Bullet> bullets;   // allocated once, contiguous.

public:
	explicit BulletPool(size_t n) : bullets(n) {}
	Bullet* acquire() {
		for (Bullet& b : bullets)
			if (!b.active) { b.active = true; return &b; }
			return nullptr;        // pool exhausted
	}
	void release(Bullet* b) { b->active = false; }
};
```

# Data-oriented design: patterns VS cache locality:

An important performance cave at for hot simulation loops.

Following a pointer to somewhere for away in memory is a ***cache miss*** - the CPU stalls waiting for RAM.

A design full of pointer-linked objects scattered across the heap (pointer chasing) can be far slower than the same data laid out contiguously.

- Array of Structs (A0S): `std::vector<Pointer>` - each particle's