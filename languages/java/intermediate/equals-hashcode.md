# Equals and hashcode

- Both are defined in the object class
- The equals method checks equality based on the reference the object is poiinting at.
- We can overide the equals methods, and we generally perform eqaulity on the fields of the object.
- When we implement equals we should also implement hashcode
  - Why?????
-

## Testing equals and hashcode

- Implementing equals must test the following
  - reflexive: an object must equal itself
  - symmetric: x.equals(y) must return the same result as y.equals(x)
  - transitive: if x.equals(y) and y.equals(z) then also x.equals(z)
  - consistent: the value of equals() should change only if a property that is contained in equals() changes (no randomness allowed)

## Violating the equals symetry

- This can be done by inheritance.
- A class which inherits from the parent class which has already overriden equals, and the child class overrides equals again with different implementation
- this leads to performing equals between the parent and child class's objects will not give correct outputs.
  -  a.equals(b) != b.equals(a) where a is subclass of b

## contracts 

- https://www.baeldung.com/java-equals-hashcode-contracts
