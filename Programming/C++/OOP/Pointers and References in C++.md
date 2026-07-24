Pointers and references are two ways in C++ lets you work with an object ***indirectly*** - through its address instead of through a copy.

In everyday application code you can avoid them, but in ***games***, ***simulations*** and ***engines*** they are unavoidable: you use them to ***control memory***, ***avoid copy large objects every frame***, ***share state between systems***, and get runtime polymorphism for entry hierarchies.

This note builds up from the memory model, then covers ***pointers***, ***references***, ***const***, ***function params***, ***dynamic memory***, ***smart pointers***, ***polymorphism***, and finally concrete game/simulation patterns and pitfalls.

# Why this matters for games and simulations:

**No hidden copies in the loop**: A simulation updates thousands of objects per time

Passing a big `Transform` or `Mesh` by value copies it every call. Passing by reference or pointer passes only an address (usually 8 bytes).

**Shared state between systems**: The physics system, the renderer, and the AI all need to look at the same entity, not private copies. Indirection lets many systems see one object.

**Runtime polymorphism**: `Enemy`, `Player`, `Projectile` all derive from `Entity`. To call the right `update()` at runtime you must go through a base-class pointer or reference.

**Explicit ownership and lifetime**: Engines create and destroy objects constantly. Pointers (especially smart pointers) let you express ***who owns what and when it dies***.

# Memory model: stack VS heap:

Every object ***lives at some address in memory***. There are two regions you care about:

**Stack** - automatic storage. Local variables live here. Fast, freed automatically when the scope ends. Limited in size.
**Heap** - (free storage) - dynamic storage. You request memory explicitly and it says alive until you release it.

Larger, but slower to allocate and your responsibility to free.

```cpp
void example() {
	int a = 10;               // 'a' lives on the stack, freed at end of function
	int* p = new int(20);     // the int lives on the heap; 'p' (on the stack) holds its adderess
	delete p;                 // you must free heap memory manually, or use a smart pointer.
}
```

A pointer or reference is just a way to name an address so you can reach the object living there.

# Pointers:

A ***pointer*** is a variable whose value is the memory address of another object.

## Declaring and using a pointer:

Three operations matter:

`*` - in a declaration means "pointer to";
`&` - (address-of) gives you the address of an object;
`*` - (dereference) gives you the object a pointer points to.

```cpp
int hp = 100;
int* p = &hp;    // p holds the address of hp
// "p" is a pointer to int, initiaized with the address of hp

std::cout << p;  // prints an address, e.g. 0x7ffc...
std::cout << *p; // prints 100 -> dereference the value AT that address

*p = 75;         // writes through the pointer; now hp == 75
std::cout << hp; // prints 75
```

Read `*p` as "the thing p points to". Writing to `*p` modifiers the original object, because the pointer refers to the same memory.

## `nullptr` - a pointer to nothing:

A pointer that doesn't point at a void object should be `nullptr` (modern C++ prefer it over the `NULL` or `0`).

```cpp
int* target = nullptr;    // points to nothing yet
if (target != nullptr) {
	// always check before dereferencting
	attack(*target);
}
// shorthabd: if (target) {...}
```

Dereferencing a `nullptr` (`*target` when `target == nullptr`) is ***undefined behavior*** - usually a crash. Checking for null is how you model "optional" links e.g. `Entity* currentTarget` that may or may not exist.

## Reading pointer declarations:

The `*` binds to the variable, not the type. This surprises people:

```cpp
int* a, b;  // a is int* but b is a plain int
int *a, *b; // both pointers - clearer to write if this way
```

## Pointer to Pointer:

A pointer can point to another pointer. You rarely need this in game logic, but you'll see it in C-style APIs and 2D arrays.

```cpp
int x = 5;
int* p = &x;
int** pp = &p;        // pp points to p. which points to x
std::cout << **pp;    // prints 5 (dereference twice)
```

# References:

A `reference` is an ***alias*** - another name for an existing object.
Once bound, the reference is that object for all practical purposes.

```cpp
int score = 50;
int& ref = score;     // ref is now another name for score.
ref = 80;             // modifiers score through reference
std::cout << score;   // prints 80
```

Two hard rules distinguish references from pointers:

1. A ***reference must be initialized when declared***. There is no "null reference" and no uninitialized reference.
2. ***A reference can never be reseated***. After declaring and initializing.

`int& ref = score`, ref refers to `score` for is entire life.

Assigning to `ref` changes `score`; it does not wake `ref` point elsewhere:

```cpp
int a = 1, b = 2;
int& r = a;
r = b;             // this does NOT rebind r to b. It copies b's value into a. Now a == 2, and r still aliases a
```

Because a reference has no "empty" state and can't be reached, it's the safer, simpler choice when you always have exactly one valid object to refer to - most commonly as a function parameter.

# Pointers VS References - when to use which:

| Feature                            | Pointer `*T`        | Reference `T&`             |
| :--------------------------------- | ------------------- | -------------------------- |
| Can be null / "no object"          | Yes (`nullptr`)     | No, must bind to something |
| Can be reseated to another object? | Yes                 | No, bound for life         |
| Must be initialized                | No (but you should) | Yes                        |
| Syntax to access value             | `*p`, p -> member   |                            |
| Pointer ariphmetic                 |                     |                            |
| Typical size                       |                     |                            |
