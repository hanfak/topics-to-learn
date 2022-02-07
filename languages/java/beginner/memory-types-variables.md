# Memory

- Types -
  - Primitive
    - size
      - https://en.wikibooks.org/wiki/Java_Programming/Primitive_Types
    - types
      -  ```byte/short/int/long/char/boolean/float/double````
  - Reference/Objects
  - Casting
    - Can apply to objects or primitives
      - The boolean type cannot be cast to/from any other primitive type.
    - casting floating point primitives (float, double) to whole number primitives, the number is rounded down.
    - implicit Casting
      - Going from smaller range to larger range
      - `byte byteVar = 42; short shortVar = byteVar;`
      - Implicit casting happens when the source type extends or implements the target type (casting to a superclass or interface).
        - example
        ```java
        String s = "str";
        Object obj= s;
        ```
    - Explicit Casting
      - Going from larger range to smaller
      - `double doubleVar = 42.0d; float floatVar = (float) doubleVar;
      - Explicit casting has to be done when the source type is extended or implemented by the target type (casting to a subtype).
        - can produce a runtime exception (ClassCastException) when the object being cast is not of the target type (or the target's subtype).
        - example
        ```java
        Object o = "str";
        String str = (String) o;
        ```
    - promotion
      - example
      ```java
      short short1 = 1, short2 = 2;
      int int1 = 1;
      char char1 = 1;
      int1 = short1 + short2; // short is promoted to int.
      int1 = char1 + short2; // both char and short promoted to int.
      ```
    - instanceOf()
      - will check if object is instance of some class or superclass (abstract/interface)
      ```java
      Object obj = Calendar.getInstance();
      obj instanceof Object;
      obj instanceof Calendar;
      obj instanceof Serializable;
      obj instanceof Date; // false, but IDE will tell you this
      ```
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
      - Example
      ```java
      int i = 10;
      ```
        - Where the value 10 is stored in i
    - reference types with null as default
      - ie `SomeNewType instanceOfNewType;` instanceOfNewType will have value of null
      - ie `SomeNewType instanceOfNewType = new SomeNewType();` will have a reference to the object which is an instance of SomeNewType.
    - Example
    ```java
    Object obj = new Object();
    ```
      - Object is a reference type.
      - obj is the variable in which to store the new reference.
      - Object() is the call to a constructor of Object.
      - What happens
        - Space in memory is allocated for the object.
        - The constructor Object() is called to initialize that memory space.
        - The memory address is stored in obj, so that it references the newly created object.
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

## Wrappers vs primitives

- Definitions
  - A primitive data type specifies the size and type of variable values, and it has no additional methods.
    - Defaults is some value
  - Wrapper classes provide a way to use primitive data types (int, boolean, etc..) as objects.
    - Have identities separate from their value
    - Default is always null if not assigned
- Problems
  - A Boolean variable should only be true or false, but in fact has third state of null
  - If int variable has default, but this can never be true
  - If some type is null by default can lead to NPE
  - Use of Database models, can have null values, so need to use wrappers
  - Generics can only use Types and not primitives
    - prevents use of collections libraries
  - Memory issues, primitives use less than type (regarding time and space)
  - Comparasion bugs when using == and equals
  - Doing multiple boxing and unboxing, espeically in loops can lead to increased time taken
- Good practice
  - use primitives in local scope
  - Effective java suggest to use primitives over wrapped
  - Use boxed for elements, keys and values in collections



## Pass by value

- https://stackoverflow.com/questions/40480/is-java-pass-by-reference-or-pass-by-value
- https://dzone.com/articles/java-copy-shallow-vs-deep-in-which-you-will-swim
- https://www.baeldung.com/java-deep-copy
- List
  - https://stackoverflow.com/questions/23607881/returning-a-private-collection-using-a-getter-method-in-java
  - https://blog.frankel.ch/back-to-basics-encapsulating-collections/

# Soft Reference

- references to data (generally reflective) will not be garbage collected until the JVM is low on memory

## Other

- Dereferencing datatypes
-

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
