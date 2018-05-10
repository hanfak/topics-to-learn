# Memory

- Types -
  - Primitive
    - size
      - https://en.wikibooks.org/wiki/Java_Programming/Primitive_Types
    - types
      -  ```byte/short/int/long/char/boolean/float/double```
  - Reference/Objects
- Variables
  - Types
    - non-static/instance fields - naming lowercase snake case
    - static/class fields
      - Constants - naming uppercase camel case
    - local variable
      - declared and used in methods
    - parameters
      - methods
      - replaced with arguments when method is called
    - wrappers
      - https://stackoverflow.com/questions/20697868/why-we-need-wrapper-class
  - Defining/Declaring
    - Types/primitives - char/int/float etc
    - Objects/reference types
      - Common - Char, Integer, Float
      - Classes - ie String, ArrayList
        - `String aString = "Hello"`
          - same as `String aNewedUpString = new String("Hello")` but is redundent but correct way as String is not a primitive type
      - interfaces
        - Declaring a list of string using the interface rather than the implementation: `List<String> aStringList = new ArrayList<>();`
      - use created
        - ie `SomeNewType instanceOfNewType = new SomeNewType()`
    - modifers (```public/private/protected/default```)
    - ```final```
  - initialization of variables
    - primitive types with default initiliazation
      - primitives variables needs to declared and set
    - reference types with null as default
      - ie `SomeNewType instanceOfNewType;` instanceOfNewType will have value of null
      - ie `SomeNewType instanceOfNewType = new SomeNewType();` will have a reference to the object which is an instance of SomeNewType.
  - default values
    - null for objects
    - for primitive values
  - Naming conventions
    - lower case camel case for variables
    - capital snake case for Constants
  - CRUD (Create/Read/Update/Delete)
    - Although we do not delete variables
  - Pointers for objects
- equality
  - pointers/reference
    - if two objects are different instances of the same class, they will by default not be equal.
    - If two objects newed separately but with same state should be equal, then need to override the equal() method.
  - object equality

## boxing and unboxing

### Links

- https://www.developer.com/java/data/autoboxing-and-unboxing-in-java.html


### Links

- http://www.learnjavaonline.org/en/Variables_and_Types
- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/variables.html
- https://www.tutorialspoint.com/java/java_variable_types.htm
- https://www.tutorialspoint.com/java/java_modifier_types.htm
- http://tutorials.jenkov.com/java/variables.html
- http://tutorials.jenkov.com/java/data-types.html
- https://www.javaworld.com/article/2077424/learn-java/does-java-pass-by-reference-or-pass-by-value.html
- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html
- http://www.baeldung.com/java-primitives
