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


