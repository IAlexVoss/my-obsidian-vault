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
dataTypeOfMethod NameOfTheMethod (dataTypeOfParam1 param1, dataTypeOfPara1 param2) {
	// Method's actions
}
```

The definition of a parameter consists of two parts: first comes the type of the parameter and then its name.

So, let's use the parameters and for this we will change the program as follows:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Person tom = new Person();
		tom.say("Hello work"); // Hello work
		tom.say("Hello gold"); // Hello gold
	}
}

class Person {

	void say(String message) {
		System.out.println(message);
	}
}
```

Here the method `say()` now takes a single parameter called message and is of type `String`.

```Java
tom.say("Hello work");
```

Here, the `message` The string "Hello work" is passed. The values that are passed to the parameters are also called **arguments**. That is, the string "Hello work" passed in this case is an argument.

Sometimes you can find such definitions as Formal parameters and Actual Parameters. Formal parameters are the actual parameters of the method (in this case, message), and actual parameters are values that are passed to formal parameters. That is, the actual parameters are the arguments of the.

Let's look at another example where we have a method that adds two numbers:

```Java
class Program {

	public static void main(String[] args) {
		
		Calculator calc = new Calculator();
		calc.sum(1, 2);
		calc.sum(1, 3);
		calc.sum(2, 4);
	}
}

class Calculator {
	
	void sum(int a, int b) {
		System.out.println(a + b);
	}
}
``` 

# Variable Length Options

A method can accept variable length parameters of the same type. For example, we need to pass a set of numbers to the method and calculate their sum, but we don't know exactly how many numbers will be passed - 3, 4, 5, or more. Variable length parameters allow you to solve this problem:

```Java
class Program {

	public static void main(String[] args) {
		
		Calculator calc = new Calculator();
		calc.sum(1, 2, 3);
		calc.sum(1, 2, 3, 4, 5);
		calc.sum();
	}
}

class Calculator {
	
	void sum(int ...nums) {
		
		int result = 0;
		for(int n: nums)
			result += n;
			
		System.out.println(result);
	}
}
```

Look at this:

> void sum(int **...nums**)

...nums <- this is a Collection of integer numbers, and we can iterate it in for cycle.

Another high-moderate example:

```Java
class Program {

	public static void main(String[] args) {
		
		Calculator calc = new Calculator();
		calc.sum("Sum of {1, 2, 3}: " 1, 2, 3);
		calc.sum("Zero sum: ");
	}
}

class Calculator {
	
	void sum(String message, int ...nums) {
		
		System.out.print(message);
		
		int result = 0;
		for(int n: nums)
			result += n;
			
		System.out.println(result);
	}
}
```


