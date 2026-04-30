# Constructors

In addition to the usual methods, classes can define special methods, which are called designers. Constructors are called when you create a new object of this class. Typically, constructors initialise an object.

## Default constrictor

If no constructors are defined in a class, a parameterless constructor is automatically created for that class. For example:

```Java
class Program {

	public static void main(String[] args) {
		
		Person tom = new Person();
		
		tom.name = "Tom";
		tom.age = 41;
		
		tom.print();
	}
}

class Person {
	
	String name;
	int age;
	
	void print() {
		
		System.out.printf("Name: %s; Age: %d\n", name, age);
	}
}
```

The above defined Person class does not have any constructors. Therefore, a default constructor is automatically created for it, which we can to create a Person object.

# Creating constructors

If you want some logic to be done when creating an object, for example, for the fields of a class to receive certain values, then you can Define your constructors in the class. At the same time, if a class defines its own constructors, then this class is deprived of Default constructor.

At the code level, the constructor represents a method named after a class that can have parameters, but does not need to define a return type. For example, let's define a simple constructor in the Person class:

```Java

```