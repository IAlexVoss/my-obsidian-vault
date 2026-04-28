In Java, exists the next following types of cycles:
- **for**
- **while**
- **do... while**

# The for loop

The for loop has the following formal definition:

```Java
for ([count initialize]; [condition]; [cange counter]) {
	instructions
}
```

Example of the most common for loop:

```Java
for (int i = 1; i < 9; i++) {
	System.out.printf("The square of number %d equals %d \n", i, i * i);
}
```

We don't have to specify all the conditions when declaring a cycle. For example, you can write like this:

```Java
int i = 1;
for (; ;) {
	System.out.printf("The square of number %d equals %d \n", i, i * i);
}
```

It's the infinity loop, because this construction don't have any condition, and don't have any counter.

Or you can omit a number of blocks:

```Java
int i = 1;
for (; i < 9;) {
	System.out.printf("The square of number %d equals %d \n", i, i * i);
	i++;
}
```

This example is equivalent to the first example. We also have a counter, but it's created outside of the loop (it's doesn't matter). We have a loop execution condition and there is an increment of the counter already in the for block itself.

A for loop can define and manage multiple variables at once:

```Java
int n = 10;
for (int i = 0; j = n - 1; i < j; i ++; j--) {
	System.out.println(i * j);
}
```

# Nested loops:

We can nested the loops. Take a look the following example:

```Java
class Programm {

	public static void main (String[] args) {
		
		// Outside cycle
		for (int i = 1; i <= 9; i++) {
			
			// Inside cycle
			for (int j = 1; j <= 9; j++) {
				System.out.print(i * j);
				System.out.print('\t');
			}
			System.out.println(); // Move to the next line
		}
	}
}

```

Here we have an external loop (the loop `for (int i = 1; i <= 9; i++)` ), which controls the number of rows. It starts with i = 1 and continues until i reaches the value 9.

# Do loop

The do loop first executes the loop code and after it checks the condition in the while statement. And as long this condition stayed is true, the cycle repeats.

```Java
int j = 7;
do {
	System.out.println(j);
	j--;
}
while (j > 0);
```

In this case, the loop code will 7 times until j is zero.

We can also write something like this:

```Java
int j = -1;
do {
	System.out.println(j);
	j--;
}
while (j > 0);
```

In this case, the loop code will 1 time and end after it.

# While loop

Cycle while immediately checks the truth of some condition, and if the condition is true, then the loop code is executed:

```Java
int j = 6;
	while (j > 0) {
		System.out.println(j);
		j--;
	}
```

In this case, the loop code will 7 times until j bigger than zero.

# Continue and Break statements

beak keyword allows you to exit the loop at any time:

```Java
for (int i = 0; i < 10; i++) {
	if (i == 5)
		break;
	System.out.println(i);
}
```

Now let's make sure that if the number is 5, the loop doesn't end, but just moves on to the next iteration. To do this, use the **continue**:

```Java
for (int i = 0; i < 10; i++) {
	if (i == 5){
		System.out.println("This is 5!!!!!")
		continue;
	}
	System.out.println(i);
}
```

