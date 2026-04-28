For transform one variable value with some data type to other data type, you should be know this scheme:

![[data_types_transformations.png]]

This conversions can be performed automatically.

**byte** -> **short** -> **int** -> **long**

**int** -> **double**

**short** -> **float** -> **double**

**char** -> **int**

# Automatic transformations

Automatic transformations proceed by the way on following example:

```Java
int a = 2147483647;
float b = a;
System.out.println(b) //2.147483647E9
```

# Explicit Conversations

Explicit conversations proceeding by the way on following example:

```Java
long a = 4;
int b = (int) a;
```

# Transformations in Operations

Examples of transformations:

```Java
int a = 3;
double b = 4.6;
double c = a + b; // (double) a + b -> 8.6
```

Another example:

```Java
byte a = 3;
short b = 4;
byte c = (byte)(a + b);
```