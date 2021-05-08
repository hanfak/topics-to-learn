# Equals and Hashcode

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Equals and Hashcode](#equals-and-hashcode)
	- [Why override them](#why-override-them)
	- [When to override](#when-to-override)
	- [When not to override](#when-not-to-override)
	- [Contract of Equals](#contract-of-equals)
	- [How to override Equals()](#how-to-override-equals)
		- [links](#links)
	- [Equals ==](#equals-)
	- [How to override hashcode](#how-to-override-hashcode)
	- [Contract of hashcode](#contract-of-hashcode)
	- [Contract of hashcode and equals](#contract-of-hashcode-and-equals)
		- [override both hashcode and equals](#override-both-hashcode-and-equals)
	- [Why test](#why-test)

<!-- /TOC -->

- https://www.baeldung.com/java-equals-hashcode-contracts

## Why override them

- By default, each object has an equals() method, this does equality check on the object
  - So two object will be different if the actual created object is unique, they will have two different references.
  - two objects are equal if and only if they are stored in the same memory address.
- By default, hascode returns an integer representation of the object memory address
  - this method returns a random integer that is unique for each instance.
  - this integer might change between several executions of the application and won't stay the same.
- Equals
  - To remove object reference equality and have equality on state
  -  it enables instances to serve as map keys or set elements with predictable, desirable behavior
- Hashcode

## When to override

- It is when a class has a notion of logical equality that differs from mere object identity and a superclass has not already overridden equals
  - case for value/domain classes
  - ie String objects of same value (ie "hello") should be equal by definition of their value

## When not to override

- If not a domain object or type
- Each instance of the class is inherently unique
  - ie Thread that represent active entities rather than values
- There is no need for the class to provide a “logical equality” test.
  - ie java.util.regex.Pattern does not override, is a design decision
- A superclass has already overridden equals, and the superclass
behavior is appropriate for this class
  - ie Set inherits from AbstractSet
- The class is private or package-private, and you are certain that its
equals method will never be invoked.
  - To completely avoid this can override it  like
  ```java
  @Override
  public boolean equals(Object o) {
    throw new AssertionError(); // Method is never called
  }
  ```
- Enums or value classes that uses instance control to ensure that at most one
object exists with each value
  - as logical equality is the same as object identity

## Contract of Equals

- laws of equality
  - Reflexive:
    - For any non-null reference value x, x.equals(x) must return true
  - Symmetric:
    - For any non-null reference values x and y, x.equals(y) must return true if and only if y.equals(x) returns true
  - Transitive:
    - For any non-null reference values x, y, z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) must return true
  - Consistent:
    - For any non-null reference values x and y, multiple invocations of x.equals(y) must consistently return true or consistently return false, provided no information used in equals comparisons is modified
    -  should perform only deterministic computations on memoryresident objects.
    - ie java.net.URL violates this, as equals uses the ip address of the hosts, and this can be different if it compares with url which gets a different ip from a source (ie dns)
  - Non-nullity
    - For any non-null reference value x, x.equals(null) must return false
- All these laws must be tested
- For an equals method to be useful, all of the elements in each equivalence class must be interchangeable from the perspective of the user.

##  How to override Equals()

- Need:
  - Use the == operator to check if the argument is a reference to this object
    - If so, return true
    - For performance
  - Use the instanceof operator to check if the argument has the correct type
    - If not, return false.
    - Typically, the correct type is the class in which the method occurs.
    - Occasionally, it is some interface implemented by this class. Use an interface if the class implements an interface that refines the equals contract to permit comparisons across classes that implement the interface.
      - ie Map, List
  - Cast the argument to the correct type.
    - Because this cast was preceded by an instanceof test, it is guaranteed to succeed.
  - For each “significant” field in the class, check if that field of the argument matches the corresponding field of this object
    - If all these tests succeed, return true; otherwise, return false.
    - If the type is an interface, you must access the argument’s fields via interface methods
    - If the type is a class, you may be able to access the fields directly, depending on their accessibility
    - primitive fields, use ==, for non float/double
    - For float/double , use Float.compare or Double.compare
      - using Float.equals, leads to autoboxing on every comparsion
    - Use Objects.equals to avoid null pointer if they contain null
    - Performance can depend on the order the fields are compared
    - You must not compare fields that are not part of an object’s logical state
    - You need not compare derived fields, which can be calculated from “significant fields”
      - doing so may improve the performance of the equals method
- IDE generation
  - Generally preferable
  - can be verbose and less readable
  - Help avoid mistakes in custom ones
  - But need to have tests
    - does not track changes in the class automatically
- Use of libraries
  - lombok
  - Apache commons

### links

- https://techrocking.com/how-to-write-equals-method-in-java/

## Equals ==

- Tests only object reference
- use for primitive
- With Integer
	- Java keeps a cache (default 128) on integers
	- Creating Integer(1) and Integer("1"), they are == the same as the refere to the same object from the cache
	- Creating Integer(1000) and Integer("1000"), they are not == the same as the refer to the different objects (as they cannot use the cache) and two new integer objects are created
- Args from main and Strings
	- if args[0] (is "hello") and "hello", then both are equals. But args[0] is an object creaed on the heap while "hello" is from the String pool. thus == will be false, but equals() will be true
	- Never use ==
	- When Strings are concat using + in a field, this will be done at compile time, but when done in say predicate of if argument this will be done at runtime hence createing different object. Thus different == will return false when comparing the field with the one created at runtime

## How to override hashcode

- https://techrocking.com/how-to-write-hashcode-in-java/

- Use of libraries
  - lombok
  - Apache commons

## Contract of hashcode

- TBC - effective java


## Contract of hashcode and equals

- If two objects are equal according to the equals(Object) method, then calling the hashcode() method on each of the two objects must produce the same integer result.
- developers should override both methods in order to achieve a fully working equality mechanism — it's not enough to just implement the equals() method.

### override both hashcode and equals

- If hashcode is not also overridden at the same time as equals, then collections that use the hashcode, will find that hashcode will create a new value for equal objects (that which was defined by user overidden equals() method)
  - This leads to, for example a hashset, containing two different elements but are defined as equals, but they should not be (due to Set contract). As the hashset uses the hashcode define uniqueness
- Contract
  - When the hashCode method is invoked on an object repeatedly during an execution of an application, it must consistently return the same value, provided no information used in equals comparisons is modified.
    - This value need not remain consistent from one execution of an application to another
  - If two objects are equal according to the equals(Object) method, then calling hashCode on the two objects must produce the same integer result.
  - If two objects are unequal according to the equals(Object) method, it is not required that calling hashCode on each of the objects must produce distinct results. However, the programmer should be aware that producing distinct results for unequal objects may improve the performance of hash tables
- Override both or none

## Why test

- To make sure changes to the object (number of fields, change of type) do not break these methods
- Do not have to test if using proven library ie lombok
- There ar libraries that test your equals method (https://jqno.nl/equalsverifier/)
