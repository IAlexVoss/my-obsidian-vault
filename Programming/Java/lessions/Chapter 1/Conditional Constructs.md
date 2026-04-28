The Java language has conditional constructs for this purpose: the **if-else** statement and the ternary operator **?:**
# If/Else construct

The **if-else** statement checks the truth of a certain condition and, depending on the result of the check, executes a certain block of code. Its simplest form consists of a single **if** block:

```Java
if(condition){
	executable instructions
}
```

The condition represents a value of type **boolean**. If the condition is **true**, then the code inside the block is executed.

Example:

```Java
class Programm {

	public static void main(String[] args) {
		
		int num1 = 6;
		int num2 = 4;
		if (num1 > num2) {
			System.out.println("The number " + num1 + " is greater than the number " + num2);
		}
	}
}
```

If the **if** block contains only a single statement, we can shorten **it** by removing the curly braces:

```Java
class Programm {
	public static void main(String[] args) {
		
		int num1 = 6;
		int num2 = 4;
		if (num1 > num2)
			System.out.println("The number " + num1 + " is greater than the number " + num2);	
	}
}
```

## The else block

If the condition is false, we can add the **else** keyword to handle the alternative case:

```Java
class Programm {
	public static void main(String[] args) {
		
		int num1 = 6;
		int num2 = 40;
		if (num1 > num2) {
			System.out.println("The number " + num1 + " is greater than the number " + num2);
		} else {
			System.out.println("The number: " + num1 + " isn't greather than number: " + num2);	
		}
	}
}
```

## Else if

To handle more conditions within a single **if** block, you can use **else if** instead of a plain **else**. You may also include a final **else** at the end of the **if-else** chain:

```Java
class Programm {
	public static void main(String[] args) {
	
		int num1 = 6;
		int num2 = 6;
		if (num1 > num2) {
			System.out.println("The number " + num1 + " is greater than the number " + num2);		
		} else if (num1 < num2) {
			System.out.println("The number: " + num1 + " is smaller than number: " + num2);	
		} else {
			System.out.println("These numbers are equal");	
		}
	}
}
```

If necessary, you can add multiple else if statements:

```Java
class Programm {
	public static void main(String[] args) {
		
		String name = "Eugene";
		
		if (name == "Tom")
			System.out.println("Your name is Tomas");
		else if (name == "Bob")
			System.out.println("Your name is Robert");
		else if (name == "Mike")
			System.out.println("Your name is Michael");
		else
			System.out.println("Unknown name");
	}
}
```

# Ternary Surgery

The ternary operation has the following syntax:

> [first operand - condition] ? [second  operand] : [third operand]

Example:

```Java
int x = 3;
int y = 2;
int z = (x < y) ? (x + y) : (x - y);
```

Is x smaller than y? If true, execute this instruction:
> x + y

If false, execute that instruction:
> x - y (the instruction after (x + y))