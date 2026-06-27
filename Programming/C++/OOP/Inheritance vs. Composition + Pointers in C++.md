
## The Core Distinction:

* Inheritance models "is-a" - `Sphere` is a `Shape`
* Composition models "has-a" - `Space ship` has a `Transform`, has a `Mesh`, has a  `Velocity`
  
```cpp
// Inheritance: Player IS-A Entity
class Player : public Entity {/* ... */};

// Composition: Player HAS-A Transform, HAS-A Mesh
class Player {
	Transform transform;
	Mesh mesh;
};
```

## Full Comparison Table:

| Aspect                 | Inheritance                                            | Composition                        |
| :--------------------- | ------------------------------------------------------ | ---------------------------------- |
| Relationship           | "is-a"                                                 | "has-a" / "uses-a"                 |
| Coupling               | Tight-child knows base's internals (protected members) | Loose-only public inheritance used |
| Flexibility at runtime | Fixed at compile time (mostly)                         | Can swap parts at runtime          |
| Code reuse             | Reuses behavior by extension                           | Reuses behavior by delegation      |
| Polymorphism           | Built-in via virtual functions                         | Requires explicit interfaces       |
| Memory layout          | Single contiguous block (base + derived)               | Parts may                          |