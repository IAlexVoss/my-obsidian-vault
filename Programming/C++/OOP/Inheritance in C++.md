
Inheritance lets a new class (the **derived**/**child** class) reuse and extend an existing class (the **base**/**parent** class).

This models "is-a" relationships - a **Dog** is an **Animal**, a **Car** is a **Vehicle**.

## Basic Syntax:

```cpp
class Base {
public:
	int x;
	void greet() { std::cout << "Hello from Base\n"; }
};

class Derived : public Base {  // Derived inherits from Base
public:
	int y;
};
```

The main pattern is:

```cpp
class ChildName : access_mode ParentName { ... };
```

**The derived class automatically gets all of the base's members:**

```cpp
Derived d;
d.x = 5;        // inherited from Base
d.y = 10;       // own member
d.greet();      // inherited function
```

## Inheritance Access Modes:

The keyword between ":" and the base name (**public**, **protected** or **private**) controls how base's members are exposed through the derived class

This is different from member access specifiers - it's about **how inheritance itself behaves**

| Base member is ... | **public** inheritance | **protected** inheritance | **private** inheritance |
| :----------------- | ---------------------- | ------------------------- | ----------------------- |
| public             | stays public           | becomes protected         | becomes private         |
| protected          | stays protected        | stays protected           | becomes private         |
| private            | not accessible         | not accessible            | not accessible          |

### A few key points:

* **public** **inheritance** is by far the most common - it models a true "is-a" relationship and keeps the inheritance intact. Use this 95% of the time.
* **private / protected inheritance** model "implemented in terms of" rather than "is-a". They're rarer and usually composition is a better choice.
* Note that a base class's **private** members are never directly accessible in the derived class, regardless of mode. That's what **protected**  is for - it's like private, but visible to derived classes.

C++ example:

```cpp
class Base {
private: int secret;
protected: int family;
public: int open;
};

class Derived : public Base {
	void test() {
		// secret = 1;      // error
		family = 2;         // ok
		open = 3;           // ok
	}
};
```

## Forms of inheritance:

### 1. Single inheritance:

One base, one derived. The simplest form

```cpp
class Animal { /* ... */ };
class Dog : Animal { /* ... */ };
```

### 2. Multilevel Inheritance:

A chain - derived from derived

```cpp
class Animal { /* ... */ };
class Mammal : public Aniimal { /* ... */ };
class Dog : public Mammal { /* ... */ };
```

### 3. Hierarchical Inheritance:

Multiple classes inherit from one base.

```cpp
class Animal { /* ... */ };
class Dog : public Animal { /* ... */ };
class Cat : public Animal { /* ... */ };
class Cow : public Animal { /* ... */ };
```

### 4. Multiple Inheritance

One class inherits than several cases at once. ( C++ allow that; many languages don't).

```cpp
class Camera { public: void takePhoto() {} };
class Phone { public: void makeCall() {} };

class SmartPhone : public Camera, public Phone {
	// has both takePhoto() and make Call() methods.
}
```

### 5. Hybrid Inheritance:

A mix of the above - which can lead to the famous **diamond problem** (covered below).

## Constructor & Destructor Order:

When you create a derived object, **constructors run base first, then derived**

Destructors run in the **reverse** order.

```cpp
class Base {
public:
	Base() { std::cout << "Base built\n"; }
	~Base() { std::cout << "Base destroyed\n"; }
};

class Derived : public Base {
public:
	Derived() { std::cout << "Derived built\n"; }
	~Derived() { std::cout << "Derived destriyed\n"; }
};

int main() {
	Derived d;
}
```

What the console returns:

```console
Base built
Derived built
Derived destriyed
Base destroyed
```

To pass arguments to a base constructor, call it in the **initializer** list:

```cpp
class Animal {
public:
	std::string name;
	Animal(std::stirng n) name(n) {}
};

class Dog : public Animal {
public:
	Dog(std::string tnt) : Animal(n) {} //forward to base constructor
};
```

## Polymorphism & Virtual Functions (the important part):

This is the reason inheritance is so powerful. A **virtual function** lets a derived class override behavior, and lets you call the correct version through a base class pointer or reference at run time.

In the next example we have three classes:
	Animal,
	Dog,
	Cat,

and **Dog** and **Cat** classes is derived classes.
	Dog -> Animal
	&
	Cat -> Animal

do an example:

```cpp
class Animal {
public:
	virtual void speak() {
		std::cout << "Some sound\n";
	}
};

class Dog : public Animal {
public:
	void speak() override {
		std::cout << "Woof\n";
	}
};

class Cat : public Animal {
public:
	void speak() override {
		std::cout << "Meow\n";
	}
};
```

Now watch what happens through a base pointer:

```cpp
Animal* a = new Dog();
a -> speak();              // "Woof" <- runtime picks Dog's version

a = new Cat();
a -> speak();              // "Meow"

// Treating different types uniformly:
std::vector<Animal*> zoo = {new Dog(), new Cat()};
for (Animal* animal : zoo) animal -> speak();        // each prints its own sound
```

Without `virtual`, `a -> speak()` would always call `Animal::speak()` based on the pointer's type, not the actual object's type.

The difference (static vs. dynamic dispatch) is the heart of polymorphism

The `override` key word (C++ 11+) is optional strongly recommended - it makes the compiler verify you're actually something catching typos and signature mismatches.

## Virtual Destructors (a common pitfall)

If you delete a derived through a base pointer, **the destructor must be virtual**, or you'll only run the base destructor - leaking the derived part.

```cpp
class Base {
public:
	virtual ~Base() {} // Always do this if the class will be inherited
};
```

> **Rule of thumb**: if a class has **any** virtual function, give it a virtual destructor.

## Abstract Classes & Pure Virtual Functions:

A **pure virtual functions** (=0) has no implementation and forces derived classes to provide one.

A class with at least one becomes an **abstract class** - you can't instance it directly.

This is how you define interfaces:

```cpp
class Shape {
public:
	virtual double area() const = 0;    // pure virtual -> abstract class
	virtual ~Shape() {}
};

class Circle : public Shape {
	double radius;
public:
	Circle(double r) : radius(r) {}
	double area() const override {
		return 3.14159 * radius * radius;
	}
};

// Shape s;    // Error: can't instance abstract class
Shape* s = new Circle(5);    // Ok
std::cout << s -> area();
```

## The Diamond Problem & Virtual Inheritance




