Java is an object-oriented language, so concepts such as "class" and "object" play a key role in it. Any Java program can be represented as a set of objects that interact witch each other.

A template or description of an object is **Class**, and the object represents an instance of that class. The following analogy can also be drawn. We all have some idea of a person - the presence two arms, two legs, a head, a body, etc. Template - This template can be called a class. A really existing person (in fact, an instance of a given class) is an object of this class.

In principle, classes have already used before. For example, in previous topics, we defined a Program class that defined all the rest of the application's code. For example:

```Java
class Program {
	
	public static void main(String[] args) {
		
		System.out.println("Hello METANIT.COM");
		System.out.println("And thenk you for all");
	}
}
```

# Defining class

A class is defined using a keyword **Class**, followed by the class name:

```Java
class class_name {

}
```

The name of the class follows the same rules as the variables' names. But in general, there is a convention in Java that class names usually begin with a capital letter.

For example, let's define a class with name Person (Person class):

```Java
class Program {
	
	public static void main(String[] args) {
		
	}
}

class Person{}
```

Classes in Java represent separate types of data. And when we define a new class that doesn't even do anything and doesn't have any content, we're actually defining ***a new type of data***. And as standard and existing Java data types, <mark class="hltr-r">we also can define variables of that type</mark>.

For example:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom; // define a new variable of class Person
	}
}

class Person {} // Person class
```

But, <mark class="hltr-r">it's not creating a new object of class Person</mark>, <mark class="hltr-g">we simply created the variable of Person class</mark>.
For define any object, we need a **new** keyword and Class Constructor.

To create an object, use **Constructors**. Constructors are essentially special methods, named after a class, that are called when a new class object is created and initialise the object. General Constructor Call Syntax:

```Java
new class_constructor(params);
```

First comes the operator **new**, which allocates memory for an object, followed by a call **Designer**.****

## Default constructor

If no constructors are defined in a class (as is the case with our empty Person class), then an empty one is automatically created for that class **Default constructor**, which does not accept No parameters. Therefore, let's use the default constructor to create an object of the Person class:****

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person(); // define a new object of class Person
	}
}

class Person {}
```

To create a Person object, you use the new Person(). As a result, after this expression is executed, a memory area will be allocated where all the data of the Person object will be stored. And the tom variable will receive a reference to the created object, and through this variable we can use this object and access its functionality.

But while we haven't defined any functionality in the Person class, Java allows us to output the object to the console:

```Java
class Program {

	public static void main(String[] args) {
		
		Person tom = new Person();
		System.out.println(tom);
	}
}

class Person {}
```

In this case, Java outputs some textual representation of an object of type "Person@1dbd16a6".

# Class  Fields

Any class may have any fields. Class Fields - it's the variables of the class object.

Some example:

```Java
class Person {
	
	String name;
	int age;
}
```

Any person have the name and age.