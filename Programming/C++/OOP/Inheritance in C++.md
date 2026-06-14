
Inheritance lets a new class (the **derived**/**child** class) reuse and extend an existing class (the **base**/**parent** class).

This models "is-a" relationships - a **Dog** is an **Animal**, a **Car** is a **Vehicle**.

## Basic Syntax:

```cpp
class Base {
public:
	int x;
	void greet() { std::count << "Hello from Base\n"; }
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

One class inherits than several vases at once. ( C++ allow that; many languages don't).

```cpp
class Camera { public: void takePhoto() {} };
class Phone { }
```