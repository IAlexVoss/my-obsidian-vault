
This is one of the most important skills for keeping projects clean as they grow.

## How C++ Complain Actually Works:

Unlike Python or JavaScript C++ doesn't have "modules" in the traditional sense (well C++ 20 added them, but most projects still use the classic model).

### Instead it has a ***two-stage*** process:

### 1. Preprocessing + Compilation - each `.cpp` file is compiled independently into an object file (`.o` or `.obj`).

The compiler sees only that one `.cpp` and whatever `#include`'s pull in.

### 2. Linking - the linker combines all objects files into one executable, resolving references between them.

The compiler processes catch `.cpp` file in isolation. So if main.cpp wants to use a `Sphere` class defined in `sphere.cpp`, it needs to know about `Sphere` - its name, its members, its method signature - without seeing the implementation.

That's what header files are for:

## Headers AND Source files:

| File type | Extension | Contains                                                          | Purpose                                                 |
| :-------- | --------- | ----------------------------------------------------------------- | ------------------------------------------------------- |
| Header    | .h/.hpp   | Declarations - class definitions, functions signatures, constants | Tells other files "this exists, here's how to call it". |
| Source    | .cpp      | Definitions - function bodies, the actual code                    | Implements what the header promised                     |

### Three rules of thumb:

Header = "what is it"
Source = "how it works"

Other files `#include` the header to learn about your class, then the linker hooks up the implementation from the source file.

## The Core Rules:

### Rule 1: Header guards (or `#pragma once`)

If two files both include the same header, the compiler would see the same code twice and complain.

Prevent this with either:

```hpp
// Classic style - works everywhere
#ifdef SPHERE_HPP
#define SPHERE_HPP

// ... header contents ...

#endif
```

Or the modern, simpler form:

```hpp
#pragma once

// ... header content ...
```

`#pragma once` isn't technically standard but every modern compiler supports it.
I recommend it - less noise, can't be typos

### Rule 2: Only declaration in headers, definitions in sources

```hpp
// sphere.hpp - DECLARES
class Sphere {
public:
	void update(float dt); // decalration only - no body
};
```

```cpp
// shpere.cpp - DEFINES
#include "sphere.hpp"
void Sphere::update(float dt) {
	// actual implementation
}
```

The `Sphere::` syntax tells the compiler "this is the implementation of `update`" belonging to class `Sphere`.

***Exceptions*** (things that do go un ***headers***):

> Class definitions themselves (their structure must be visible).
> `inline` functions and very short methods.
> `constexpr` constants.
> Templates (they must be visible to every file that uses them - additional topic).

### Rule 3: Never `#include` a `.cpp` file

Only include `.hpp`/`.h`. Including a `.cpp` causes the linker to see the same code twice -> "multiple definition" errors.

### Rule 4: Avoid ***using namespace*** in headers:

If a header says using namespace std; every file including it inher