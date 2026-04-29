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

Keywords `public` and `static` are modifiers. Next is the return type.