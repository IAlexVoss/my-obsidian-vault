__Java is a strongly typed language__ - <mark class="hltr-b">any variable and constant represent a certain type and this type as strictly defined.</mark>
# Integer Data Types in Java

<mark class="hltr-g">Note: 0000 - it's a tetrad</mark>

#### <mark class="hltr-r">byte</mark> - stores an integer from -128 up to 127 and takes 1 byte
	1 byte: 0000 0000 

```Java
byte x = 8;
byte y = 2;
```
#### <mark class="hltr-r">short</mark> - stores an integer from -32768 up to 32767 and takes up 2 bytes
	2 bytes: (0000 0000) + (0000 0000)

```Java
short x = 1000;
short y = 2331;
```
#### <mark class="hltr-r">int</mark> - stores an integer from -2147483648 up to 2147483647 and takes 4 bytes
	4 bytes: (0000 0000) x4 = (0000 0000) + (0000 0000) + (0000 0000) + (0000 0000)

```Java
int x = 435_344;
int y = 344_233;
```
#### <mark class="hltr-r">long</mark> - stores an integer from -9 223 372 036 854 775 808 up to 9 223 372 036 854 775 807 and occupies 8 bytes
	8 bytes: (0000 0000) x8

```Java
long num1 = 9_894_984_123l;
long num2 = -3_334_574_123l;
```
# Floating-point Data Types

#### <mark class="hltr-r">double</mark> - stores a floating-point number from ± $4.9 * 10^{-324}$  up to ± $1.7976931348623157 * 10^{308}$ and takes up 8 bytes
	8 bytes: (0000 0000) x8

```Java
double x = 4.5;
double y = 4.1;
```
#### <mark class="hltr-r">float</mark> - stores a floating-point number from $-3.4*10^{38}$ up to $3.4*10^{38}$ and takes up 4 bytes
	4 bytes: (0000 0000) x4

```Java
float x = 4.5F;
float y = 4.1F;
```

# Symbolic Data Types

#### <mark class="hltr-r">char</mark> - stores a single character in UTF-16 encoding and occupies 2 bytes, so the range of stored values from 0 up to 65535
	2 bytes: (0000 0000) x2

```Java
char charA = 'A';
char randChar = '126';
```

#### <mark class="hltr-r">String</mark> - it's not regular data type, because it's a class in Java. However, String object - it's object who stored chars arrays

```Java
String name = "Alex";
String text = """
			  Вот мысль, которой весь я предан,
              Итог всего, что ум скопил.
              Лишь тот, кем бой за жизнь изведан,
              Жизнь и свободу заслужил.
			  """
```