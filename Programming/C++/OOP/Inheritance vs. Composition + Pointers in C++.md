
## The Core Distinction:

* Inheritance models "is-a" - `Sphere` is a `Shape`
* Composition models "has-a" - `Space ship` has a `Transform`, has a `Mesh`, has a  `Velocity`
  
```cpp
// Inheritance: Player IS-A Entity
class Player : public Entity {/* ... */};

// Composition: Player HAS-A Transform, HAS-A Mesh
class Player {
	Transform transform;
	Mesh
}
```