Methods can return some value. In the examples in the previous articles, we used methods that had the type `void`: Methods with this type do not return any value. They just perform some actions. To return a certain result, the method uses the **return**:

```java
return returned_value;
```

After the operator **return** specifies the return value that is the result of the method. This can be a literal value, a variable value, or of some complex expression.

For example, let's define a method that returns a value of the `String`:

```Java
class Perosn {
	
	String sayHello() {
		return "Hello";
	}
}
```

- Method `sayHello` has a type `String`, therefore, it must return a string.
- Therefore, in the body of the method The operator is used return, after which the returned string is specified.

At the same time, methods that have any type as a return type, except for void, must use return statement to return the value. For example, the following method definition is incorrect:

```Java
String sayHello() {
	
	System.out.println("Hello");
}
```

Absolutely incorrect, because method with some **Data Type** on the start method defining, NECESSARY need the RETURN  with the same value Data Type on returning value

We can assign the result of methods that return a value to variables or otherwise use them in the program:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person();
		System.out.println(tom.sayHello()); // Hello
		
		String message = 
	}
}
```
