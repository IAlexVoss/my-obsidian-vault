Arrays uses for store data in the some dimensional lists.

{1, 2, 4, 5, 6} - One dimensional array
{{1, 2, 3, 4}, {1, 2, 3, 4}} - two dimensional array
{ { {1, 2, 3, 4, 5}, {1, 2, 3, 4, 5} }, { {1, 2, 3, 4, 5}, {1, 2, 3, 4, 5} } } - three dimensional array

{ {1, 2, 3}, {1, 2, 3, 4, 5, 6}, {1, 2, 3, 4}} - Jagged array, or 2 dimensional array like this:
{ {1, 2, 3, 0, 0, 0}, {1, 2, 3, 4, 5, 6}, {1, 2, 3, 4, 0, 0} }

**How to create constructions like it, in Java?**

# Declaring and defining the array

For defining the array, use followed representation:

```Java
data_type name_of_the_array[];
// or
data_type[] name_of_the_array;
```

If you need declare multiple arrays, **use** the next representation:

```Java
int[] arr1, arr2, arr3;
```

If the array is defining, we can initialize it:

```Java
int nums[];
nums = new int[4]; // array with 4 potentional numbers 
```

And we also can initialize array and defining it simultaneously:

```Java
int nums[] = new int[4];
int[] nums2 = new int[5];
```

Another way to initialize the array:

```Java
int nums = new int[] {1, 2, 3, 4, 5};
int nums2 = {1, 2, 3, 4};
```

For set and get value of the array element -> use an index for this:

```Java
int[] nums = new int[4]; // emty 4 potential number array

// Set values of the array elements
nums[0] = 1;
nums[1] = 2;
nums[2] = 3;
nums[3] = 4;

// Get values from the third array element
System.out.println(nums[2]); // 3
```

# Length of the array

The most important property that arrays have is the length, returning the length of the array, that is, the number of its elements:

```Java
int[] nums = {1, 2, 3, 4, 5};
int length = nums.length; // 5
```

For defining 2-dimensional array, use the following representation:

```Java
int[][] nums = { {0, 1, 3}, {1, 2, 3} };
```

For 3-dimensional array:

```Java
int[][][] nums = new int[2][3][4] // for simpest declaring 
```

# Jagged array

Multidimensional arrays can also be represent as "jagged arrays".

```Java
int[][] nums = new int[3][];
nums[0] = new int[2];
nums[1] = new int[3];
nums[2] = new int[4];
```

In this case we have a 2-dimensional array with 3 rows and unknown count of columns, but, our array have the 2, 3 and 4 columns in the its rows.

It is looks like this:

array:
0: [0, 0]
1: [0, 0, 0]
2: [0, 0, 0, 0]

where the "zeros" are the identical numbers

# Iterating over arrays

You can use the standard loop to iterate over arrays **for**:

```Java
class Programm {

	public static void main(String[] args) {
		
		int array[] = {1, 2, 3, 4, 5};
		
		for (int i = 0; i < array.length; i++) {
			
			System.out.println(array[i]);
		}
	}
}
```

However in Java also have a special version of the loop for Designed to iterate over elements in sets, such as arrays and collections.
It is analogous to the action of the loop **foreach**, Its formal announcement:

```Java
for (name_of_the_variable : container) {
	// actions 
}
```

```Java
int[] array = { 1, 2, 3, 4, 5};
for (int i : array) {
	
	System.out,println(i);
}
```

In this case, the container is an array of data of the `int`. Then a variable of type `int`

# Iterating over multidimensional arrays in the loop

```Java
int[][] nums =
{
	{1, 2, 3},
	{4, 5, 6},
	{7, 8, 9}
};
for (int i = 0; i < nums.length; i++) {

	for (int j = 0; j < nums[i].lenght; j++) {
		
		System.out.printf("%d", nums[i][j]);
	}
	System.out.println();
}
```

Secret line, secret one