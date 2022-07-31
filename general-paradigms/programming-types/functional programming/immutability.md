## Objects should be immutable

- https://www.yegor256.com/2014/06/09/objects-should-be-immutable.html
- https://www.yegor256.com/2014/12/09/immutable-object-state-and-behavior.html
- https://reflectoring.io/java-immutables/
- https://xtrem-tdd.netlify.app/Flavours/immutable-types

## Data and objects

- Persistent collections have good characteristics in code world: they make work with them more predictable, testable and transparent.
  - That’s what makes them good for keeping identity.
  - But at data world, they lead to extra expences in terms of memory consumption and copying, and their immutable nature may cause inconveniences, when there are lots of writes on them.
- Mutable collections have decent characteristics in data world: they are fast, cheap and flexible.
  - Which make them good candidates for keeping state in memory.
  - But at code world, they are the source of undesirable side effects.
- Arguments and variables (method/fields) should be final (ie cannot be reassigned with a new value) be assigning once
  - Improves reasoning about code
  - Can lead to nulls with unset variables

## Benefits

- Concurrency
  - If we’re working with concurrent threads that access the same objects, it’s best if those objects are immutable. This way, we can not introduce any bugs that arise from accidentally modifying the state of an object in one of the threads.
  - In concurrency code, we should make objects mutable only if we have to.
- Value Objects
  - Value objects are objects that represent a certain value and not a certain entity.
  - Thus, they have a value (which may consist of more than one field) and no identity.
  - Examples for value objects are:
    - Java’s wrappers of primitives like Long and Integer
    - a Money object representing a certain amount of money
    - a Weight object representing a certain weight
    - a Name object representing the name of a person
    - a UserId object representing a certain numerical User-ID
  - Since value objects represent a specific value, that value must not change. So, they must be immutable.
    - Imagine passing a Long object with value 42 to a third-party method only to have that method change the value to 13. Can’t happen with an immutable.
- Data Transfer Objects
  - Another use case for immutables is when we need to transport data between systems or components that do not share the same data model.
  - In this case, we can create a shared Data Transfer Object (DTO) that is created from the data of the source component and then passed to the target component.
  - Although DTOs don’t necessarily have to be immutable, it helps to keep the state of a DTO in a single place instead of scattered over the codebase.
  - Imagine we have a large DTO with tens of fields which are set and re-set over hundreds of lines of code, depending on certain conditions, before the DTO is sent over the line to a remote system. In case of an error, we’ll have a hard time finding out where the value of a specific field came from.
  - If we make the DTO immutable (or close to immutable) instead, with dedicated factory methods for valid state combinations, there are only a few entry points for the state of the object, easing debugging and maintenance considerably.
- Domain Objects
  - A domain object is most certainly not immutable, but we will benefit from making it as immutable as possible.


### Links

- https://www.yegor256.com/2014/11/07/how-immutability-helps.html

## Antipatterns

- Don’t Use Builders to create immutable objects
  - trade off, depends on it's useage
- Don’t Use Withers
  ```java
  @RequiredArgsConstructor
  class User {

    private final Long id;
    private final String name;

    User withId(Long id) {
      return new User(id, this.name);
    }

    User withName(String name) {
      return new User(this.id, name);
    }

  }
  ```
  - Similar to setters
  - We’re using an immutable as if it were mutable.
- Don’t Provide Getters by Default
  - Especially on fields that are a collection, as this can still be mutated
  - Create a copy
