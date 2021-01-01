# Value objects

- AKA
  - domain objects
  - anaemic objects
- Just fields, immutable (no setters) never change
  - Equality based on values/properties of object (thus will need to override equals and hashcode) rather than identity
  - No Setters
  - Fields should be immutable as well as object graph
    - Otherwise return copy in getter
- Can hold behaviour
