switch/case evaluates the expression and compares its value to a set of values. And when the values match, it executes a certain code.

This block has the following formal definition:

```Java
switch (expression) {
	case value1:
		executable code;
		break;
	case value2:
		executable code;
		break;
	case valueN:
		executable code;
		break;
	default:
		executable code;
		break;
}
```

For example:

```Java
class Program {
	public static void main(String[] args) {
		
		String name = "Tom";
		
		switch (name) {
			
			case "Bob":
				System.out.println("Your name is Bob");
				break;
			case "Tom":
				System.out.println("Your name is Tom");
				break;
			case "Sam":
				System.out.println("Your name is Sam");
				break;
		}
	}
}
```

If we don't put break keyword into case code block, then program will be executed on next cases:

```Java
class Program {
	public static void main(String[] args) {
		
		String name = "Tom";
		
		switch (name) {
			
			case "Bob":
				System.out.println("Your name is Bob");
			case "Tom":
				System.out.println("Your name is Tom");
			case "Sam":
				System.out.println("Your name is Sam");
		}
	}
}
```

And the output then...

```Console
Your name is Tom
Your name is Sam
```

If the value does not match any of the case blocks, then, if a default block has been defined, that block will be executed:

```Java
class Program {
	public static void main(String[] args) {
		
		String name = "Samuel";
		
		switch (name) {
			
			case "Bob":
				System.out.println("Your name is Bob");
				break;
			case "Tom":
				System.out.println("Your name is Tom");
				break;
			case "Sam":
				System.out.println("Your name is Sam");
				break;
			default:
				System.out.println("Unknown name");
				break;
		}
	}
}
```

Console output:

```Console
Unknown name
```

We can make it shorter with the next scheme:

```Java
switch (expression) {
	
	case value1 -> executable_code;
	case value2 -> executable_code;
	// ...
	case valueN -> executable_code;
	default -> executable_code;
}
```

Simple example of this:

```Java
class Program {
	public static void main (String[] args) {
		
		String name = "Tom";
		
		switch (name) {
		
			case "Bob" -> System.out.println("Your name is Bob");
			case "Tom" -> Ststem.out.println("Your name is Tom");
			case "Sam" -> Ststem.out.println("Your name is Sam");
		}
	}
}
```

if you put several instructions or more complex code into the one case block, then you should be stored it's code in the one code block:

```Java
case "Tom" -> {
	System.out.println("Your name is Tom");
	System.out.println("Hello, I'm Tom!");
}
```

# Returning value from the switch

We can change outside variable in the switch construction. We can make this by the way:

```Java
class Program {
	public static void main(String[] args) {
		
		int operation = 1;
		int a = 10, b = 6;
		
		int result = 0;
		
		switch (operation) {
			
			case 1:
				result = a + b;
				break;
			case 2:
				result = a - b;
				break;
			case 3:
				result = a * b;
				break;
			default:
				System.out.println("Unknown operation");
				break;
		}
	}
}
```

And like this:

```Java
class Program {
	
	public static void main(String[] args) {
		
		int operation = 1;
		int a = 10; b = 6;
		
		int result = switch (operation) {
			
			case 1 -> a + b;
			case 2 -> a - b;
			case 3 -> a * b;
			default -> 0;
		}; // On the enb, semicolon is necessary
		
		System.out.println(result) // 16
	}
}
```

