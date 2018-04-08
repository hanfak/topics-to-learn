# Basics of java

This can be applied to practically any langauge.

## Setup the system

- Installing java/JDK
  - Knowing the difference between JDK, JRE and JVM
- Setting up the path
- Installing and setting up IDE (Intellij)
  - Can use Eclipse or Netbeans, but Intellij is far better
- Settings to use JDK
  - Create new project using maven and add java build in pom.xml
  - See ...
- Running a simple hello world program through Intellij to check it is working
```java
  public class Example {
      public static void main(String[] args) {
          System.out.println("Hello, World");
      }
  }
```
  - Use of shortcuts ie ```sout``` and ```psvm```

## Learn the basics of code

###  Computation
  - What is programming?
    - https://en.wikipedia.org/wiki/Computer_programming
  - Algorithm?
  - Pseudocode?
  - Algorithm/pseudocode -> source code -> run it to do the task
- To know
  - Compling and compilers
  - Interpreting and interpreters (for dynamic languages like Ruby, Python)
  - Byetcode
  - Running bytecode

### Memory

- Types -
  - Primitive
    - size
    - types - ```byte/short/int/long/char/boolean/float/double```
  - Reference/Objects
- Variables
  - Types
    - non-static/instance fields
    - static/class fields
      - Constants
    - local variable
    - parameters
  - Defining
    - Types/primitives - Char/Int/Float etc
    - Objects/reference types - String, created
    - modifers (```public/private/protected/default```)
    - ```final```
  - default values
    - null for objects
    - for primitive values
  - Naming conventions
    - lower case camel case for variables
    - capital snake case for Constants
  - CRUD (Create/Read/Update/Delete)
  - Pointers for objects
- equality
  - pointers/reference
  - object equality
- Data structures
  - Arrays
  - Arayslist/list
  - map/dictionary
  - set
  - linked lists
  - queues

### Instructions
  - Expression
  - Statements, order
    - ```;```
  - Boolean statements (and/or/not)
    - <, >, >=, =< , ==, !=, object.equals(anotherObject)
  - Arithmetic/math operations
    - simple operators on primitives
    - use of libraries
      - i.e. abs, ceil
      - see https://docs.oracle.com/javase/8/docs/api/java/lang/Math.html
  - Declaring and assigning Variables
  -

### Looping/Iterating
  - Repeating the same task
  - Doing the same thing across a data structure
  - ```for```/```while```/```do while``` (imperative)
    - New for each loop
      - ```for (String element : listOfStrings) {...}```
  - ```continue```
  - ```break```
  - ```exit```
  - Recursion
  - Nested loops

### Conditonal/Flow control
  - Changing the flow of instructions
  - ```Switch/Case```
  - ```Break```
  - ```if/else```
  - ```else if```
  - ```return```
  - Use of ```{}```
  - Nested if statements

### Functions/methods
  - No parameters ```String method(){...}```
  - parameters
    - varags ie ```Integer method(String... x){...}```
  - Overloading
    - ```String method(){...}```
    - ```String method(int a){...}```
  - Instance method
  - Static method
    - ```static String method() {...}```
  - ```Void```
  - Return type is declared
    - ```static String method() {... return ....}```
  - Using the above
    - creating methods
    - using methods
      - within class
      - in different class
        - ```instance.method(1);```
      - Defining variable for storing/referencing output of method
        - ```Integer a = instance.method(1);```
        - ```Integer a = method(1);```
  - variable scope
  - Naming conventions

### Printing to screen/debugging
  - ```System.out.println("Hello, World");```
  - print output of method
    - ```System.out.println(method(1));```
  - print output of variables
    - ```System.out.println(a);```

### Exercises

- [Code wars](https://www.codewars.com)

### Links/Books

Most of these links will cover way more then what has been written above

- [Codecdemy](https://www.codecademy.com/catalog/language/java)
- [tutorial point](https://www.tutorialspoint.com/java/index.htm)
- [Head first java](http://amzn.eu/70wOEbM)
- [https://learnxinyminutes.com/docs/java/](https://learnxinyminutes.com/docs/java/)
- [Oracle documentation](https://docs.oracle.com/javase/tutorial/index.html)
- https://courses.caveofprogramming.com/p/java-for-complete-beginners
- [Banas videos series](https://www.youtube.com/playlist?list=PLE7E8B7F4856C9B19)
- [Banas one video](https://www.youtube.com/watch?v=WPvGqX-TXP0&t=0s&list=PLE7E8B7F4856C9B19&index=94)
