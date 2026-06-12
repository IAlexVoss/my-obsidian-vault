
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
myDog.bark();          // call its 
```

