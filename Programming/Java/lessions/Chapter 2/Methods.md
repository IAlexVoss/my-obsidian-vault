If class variables store the state of an object, then **Methods** represent his behaviour. Methods contain a set of statements that perform specific actions. And if we need define some actions in the class, we need to define the.

# Definition of methods

The general definition of methods is as follows:

```Java
[modificators] returning_type name_of_method ([params]) {
	// method's body
}
```

Modifiers and parameters are optional.

By default, the main class of any Java program contains a main method that serves as an entry point into the program:

```Java
class Program {
	
	public static class main(String[] args) {
		
		System.out.println("Hello world");
	}
}
```

Keywords `public` and `static` are modifiers. Next is the return type. Keyword `void` indicates that the method does not return anything.

For example, let's create a class and define the:

```Java
class Person {
	
	String name;
	int age;
	
	void print() {
		
		System.out.println("Name: " + name + "\tAge: " + age + "\n");
	}
}

class Program {
	public static void main(String[] args) {
		
	}
}
```

Here, a Person class is defined with two fields, name and age, and one print method. The print iode as the return type is of type `void` (that is, in fact, it does not return anything) and does not accept any parameters. All this method does is print the values of the name and age variables to the console.

But in order to apply the method, it must be **Call**.

# Calling the

The method is called in the form:

```Java
method_name(args);
```

After the method name, there are parentheses that list the arguments - values for the method parameters.

Simple example for run:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person();
		
		tom.name = "Tom";
		tom.age = 41;
		
		tom.print(); // call print() method from the Person class for tom object
	}
}

class Person {
	
	String name;
	int age;
	
	void print() {
		Sustem.out.printf("Name: %s \tAge: %d\n", name, age);
	}
}
```

To call the print method, the main method uses the `tom.print()`. That is, as in the case of fields, the name of the class variable is followed by a period and then the name of the method. Since the print method has no parameters, empty parentheses are placed after its name. As a result, when the program is executed, we will see information about the object fields on the console:

```Console
Name: Tom          Age: 41
```

One of the advantages of the methods is that we can derive some general actions in the method and then call them repeatedly in different places in the program. For example:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person();
		
		tom.name = "Tom";
		tom.age = 41;
		tom.print();
		
		tom.name = "Tomas";
		tom.print();
		
		tom.name = "Tommy";
		tom.print();
	}
}

class Person {
	
	String name;
	int age;
	
	void print() {
		Sustem.out.printf("Name: %s \tAge: %d\n", name, age);
	}
}
```

Console output:

```Console
Name: Tom    Age: 41
Name: Tomas  Age: 41
Name: Tommy  Age: 41
```

# Calling Methods in Other Methods of a Class

Some methods of a class can call other methods of this class:

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
	
	void printName() {
		System.out.printf("Name: %s\n", name);
	}
	
	void printAge() {
		System.out.printf("Age: %d\n", age);
	}
	
	void print() {
		printName();
		printAge();
	}
}
```

Here, two other methods of the class are called in the print method, printName and printAge. Console Program Output:

```Console
Name: Tom
Age: 41
```

