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
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person();
		tom.print();
	}
}

class Person {
	
	String name;
	int age;
	
	// Constructor
	Person() {
		
		System.out.println("Creating Person object");
		name = "Tom";
		age = 41;
	}
	
	void print() {
		
		System.out.printf("Name: %s; Age: %d\n", name, age);
	}
}
```

So, here in the Person class, there is a constructor that prints some message to the console and initialises the fields of the class:

```Java
Person() {
	
	System.out.println("Creating Person object");
	name = "Tom";
	age = 41;
}
```

We can define other constructors in a class in a similar way. For example:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person();
		Person bob = new Person("Bob");
		Person sam = new Person("Sam");
		
		tom.print();
		bob.print();
		sam.print();
	}
}

class Person {

	String name;
	int age;
	
	Person() {
	
		name = "Undefined";
		age = 18;
	}
	
	Person(String username) {
		
		name = username;
		age = 18;
	}
	
	Person(String username, int userage) {
		
		name = username;
		age = userage;
	}
	
	void print() {
		
		System.out.printf("Name: %s; Age: %d\n", name, age);
	}
}
```

There are now three constructors defined in the class, each of which takes a different number of parameters and sets the values of the class fields.

Console output:

```Console
Name: Undefined  Age: 18
Name: Bob  Age: 18
Name: Sam  Age: 25
```

# Keyword this

