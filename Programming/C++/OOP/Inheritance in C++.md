
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

* **public** **inheritance** is by far the most common - it models a true "is-a" relationship and keeps 