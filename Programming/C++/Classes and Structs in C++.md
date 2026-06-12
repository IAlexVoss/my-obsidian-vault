
This is the some hints for using C++ OOP, inheritance and e.t.c.

Both **class** and **struct** let you bundle related data and functions together into a single custom type

In C++ - there's really one technical difference between then, but they tend to be used for different purposes by convention.

## The Core Idea:

A **class** or **struct** lets you define a blueprint for objects.

The blueprint describes:
	**Member variables:** (data the objects holds)
	 **Member functions:** (operations the object can perform)

Some example for explanation:

```cpp
class Dog {
public:
	std::string name;    // Member variable
	int age;             // Member variable
	
	void bark() {        // Member function
		std::cout << name << " says Woof!\n";
	}
};
```

And then, you create objects (also called instances) from this blueprint:

```cpp
Dog myDog;             // create an object
myDog.name = "Rex";    // set its data
myDog.age = 3;         
myDog.bark();          // call its function -> "Rex says woof!"
```

## The one real Difference: Default Access:

In a **class**, members are **private by default**
In a **struct**, members are **public by default**

```cpp
class MyClass {
	int x;          // Private by default - can't access from outside
};

struct MyStruct {
	int x;          // Public by default - accessible from outside
}
```

That's it Everything else they are do is identical: both support inheritance, member functions, constructors, access specifiers, e.t.c.

## Access Specifiers:

> **public**       ->            anyone, from anywhere
> **private**      ->            only the class's own member functions
> **protected** ->            the class itself and its deriver (child) classes

Example of access specifiers:

```cpp
class BankAccount {
private:
	double balance;        // hidden from outside

public:
	void deposit(double amount) {
		balance += amount; // ok - inside the class
	}
	
	double getBalance() {
		return balance;
	}
};
```

```cpp
int main() {
	BankAccount acc;
	
	// acc.balance = 1_000_000      // Error: balance is private
	
	acc.Deposit(100);               // ok: public function
}
```

This is the principle of encapsulation - hide the internal data and expose a controlled inheritance.

It's why, classes are typically preferred when you want to enforce rules about how data is used.

## Constructors:

A **constructor** is a special function that runs automatically when an object is created.

It's used to initialize the object.

```cpp
class Point {
public:
	int x, y;
	
	// Constructor
	Point (int startX, int startY) {
		x = startX;
		y = startY;
	}
};

int main() {
	Point p(5, 10); // constructor runs: x = 5, y = 10
}
```

A cleaner, preferred way uses an initializer list:

```cpp
Point(int startX, int startY) : x(startX), y(startY) {}
```

There's also a destructor (~Point()) that runs when the object is destroyed - useful for cleanly like freeing memory

## Then to Use Which (Convention):

Since they're nearly identical, programmers follow conventions:

* **struct** - for simple bundles of public data with little or no behavior (sometimes called "plain of data").
	 example: a 3D coordinate {x, y, z};
* **class** - for objects with behavior, encapsulation, and invariants to protect.
	 example: a **BankAccount** that must never go negative

Let's to watch a Full example:

```cpp
struct Color {
	int red, green, blue;
};

class Temperature {
private:
	double celsius;
	
public:
	Temperature (double c): celsius(c) {}
	double to FAHrenheit() { return celsius * 9.0/5.0 + 32.0}
};
```

Add a complex Example:

```cpp
#include <iostream>
#include <string>

class Car {
private:
	std::string model;
	int speed;
	
public:
	Car (std::string m) : model(m), speed(0) {}    // Constructor
	void accelerate(int amount) {
		speed += amount;
	}
	
	void display() {
		std::cout << model << "is going" << speed << "km/h\n";
	}
};

int main() {
	Car myCar("Toyota");
	myCar.accelerate(50);
	myCar.accelerate(30);
	myCar.display();
	return 0;
}
```

## Summary:

A **class**/**struct** groups **data** + **functions** into a custom type.

The only technical difference is default access (class -> private, struct -> public)

Use access specifiers to control visibility, constructors to initialize objects and lean on class when you want encapsulationб struct for simple data bundles