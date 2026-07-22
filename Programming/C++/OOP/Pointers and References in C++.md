Pointers and references are two ways in C++ lets you work with an object ***indirectly*** - through its address instead of through a copy.

In everyday application code you can avoid them, but in ***games***, ***simulations*** and ***engines*** they are unavoidable: you use them to ***control memory***, ***avoid copy large objects every frame***, ***share state between systems***, and get runtime polymorphism for entry hierarchies.

This note builds up from the memory model, then covers ***pointers***, ***references***, ***const***, ***function params***, ***dynamic memory***, ***smart pointers***, ***polymorphism***, and finally concrete game/simulation patterns and pitfalls.

## Why this matters for games and simulations:

**No hidden copies in the loop**: A simulation updates thousands of objects per time

Passing a big `Transform` or `Mesh` by value copies it every call. Passing by reference or pointer passes only an address (usually 8 bytes).

**Shared state between systems**: The physics system, the renderer, and the AI all need to look at the same entity, not private copies. Indirection lets many systems see one object.

**Runtime polymorphism**: `Enemy`, `Player`, `Projectile` all derive from `Entity`. To call the right `update()` at runtime you must go through a base-class pointer or reference.

**Explicit ownership and lifetime**: Engines create and destroy objects constantly. Pointers (especially smart pointers) let you express ***who owns what and when it dies***.

## Memory model: stack VS heap:



