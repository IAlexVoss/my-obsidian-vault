In the program, we can use methods with the same name, but with different types and/or numbers of parameters. Such a mechanism is called method overloading (method overloading).

For example:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Calculator calc = new Calculator();
		System.out.println(calc.sum(2, 3));
		System.out.println(calc.sum(4.3, 3.2));
		System.out.println(calc.sum(4, 3, 7));
	}
}

class Calculator {
	
	int sum(int x, int y) {
		
		return x + y;
	}
	double sum(double x, double y) {
		
		return x + y;	
	}
	int sum(int x, int y, int z) {
		
		return x + y + z;
	}
}
```

Here, the Calculator class is defined with three options or three method overloads `sum()`, but when it is called, depending on the type and number of transmitted parameters, the system will choose the version that is most suitable.

It is worth noting that the number and types of parameters affect the overload of methods. However, the difference in the type of return value for overload does not matter. For example, in the following case, the sum methods differ in the type of return value:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Calculator calc = new Calculator();
		System.out.println(calc.sum(2, 3));
	}
}

class Calculator {
	
	int sum(int x, int y) {
		
		return x + y;
	}
	// Error - method sum is already exist
	double sum(int x, int y) {
		
		return x + y;	
	}
}
```

However, this will not be considered overload. Moreover, such a program is incorrect and simply does not shrink, since a method with the same number and type of parameters is defined several times.