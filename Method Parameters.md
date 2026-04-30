With the help of parameters, we can pass various data to the methods that will be used for calculations. For example, let's define the following program:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person();
		tom.say(); // Hello
		tom.say(); // Hello
	}
}

class Person {

	void say() {
		System.out.println("Hello");
	}
}
```

Console output:

```Console
Hello
Hello
```

But no matter how much we call the say method, the result won't change. And to be able to customise the behaviour of the method externally, the parameters are applied. Parameters are defined in parentheses after the method name in the form:

```Java
dataTypeOfMethod NameOfTheMethod (dataTypeOfParam1 param1, dataTypeOfParam1 param1)
```
