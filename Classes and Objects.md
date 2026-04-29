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

For example, let's define a class with name Person (Persin class)