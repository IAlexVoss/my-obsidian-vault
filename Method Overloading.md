In the program, we can use methods with the same name, but with different types and/or numbers of parameters. Such a mechanism is called method overloading (method overloading).

For example:

```Java
class Program {
	
	public static void main(String[] args) {
		
		Calculator calc = new Calculator();
		System.out.println(calc.sum(2, 3));
		System.out.println(calc.sum(4.3, 3.2));
		System.out.println(calc.sum(2, 3));
	}
}
```