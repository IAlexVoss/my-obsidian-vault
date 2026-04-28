For using console in Java, you must be know something about Console I/O in Java
I - input
O - output
it's simple, but I should give you representation of this down here:
# Console O (Output)

To create an output stream to the System class, you define a <mark class="hltr-r">out</mark>. **println** function just allows you to print a certain value to the console and then move the console cursor to the next line.

```Java
class Program {
	public static void main(String[] args) {
		
		System.out.println("Something cool");
		System.out.println("Something else?");
	}
}
```

Console output:
```Console
Something cool
Something else?
```

If you use another function, maybe as like **System.out.print()**, which is similar to println except that does not move to the next line.

```Java
class Program {
	public static void main(String[] args) {
		
		System.out.print("Something cool");
		System.out.print("Something else?");
	}
}
```

Console output:
```Console
Something coolSomething else?
```

However, you can also use the **System.out.print()** method to move the carriage to the next line. To do this, you need to use the escape sequence <mark class="hltr-r">\n</mark>:

```Java
System.out.print("Something cool with escape\n");
```

So, you can also use the printf (like C language) function for printing something with fixed variable positions on the string like this:

```Java
int x = 5;
int y = 1;

System.out.printf("x=%d; y=%d \n", x, y);
```

In addition to the %d specifier, we can use a number or other data types:
- **%x:** to output hexadecimal numbers
- **%F**: to output floating-point numbers
- **%e**: to output numbers in exponential form, e.g., 1.3e+01
- **%C**: to output a single character
- **%s**: to output string values
- **%b** to output values of type boolean

# Console I (Input)

To receive input from console, use the System class defines a **in**. But, you also should use the "Scanner" object for use the input to console:

In code using example:
```Java
import java.util.Scanner;

class Programm {

	public static void main(String[] args) {
	
		Scanner in = new Scanner(System.in);
		System.out.print("Input a number: ");
		int num = in.nextInt();
		
		System.out.printf("Your number: %d \n", num);
		in.close(); // for close tye thread
	}
}
```

Console output:
```Console
Input a number: 5
Your number: 5
```

You can also use the a lot of another methods of Scanner object for input others values:
- **next()**: reads the entered string to the first space
- **nextLine()**: reads the entire entered string
- **nextInt()**: reads the entered int number
- **nextDouble()**: eads the entered double number
- **nextBoolean()**: reads the value of boolean
- **nextByte()**: reads the byte number entered
- **nextShort()**: reads the byte number entered

