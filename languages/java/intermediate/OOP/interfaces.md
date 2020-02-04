# Interfaces

## What?

- is an abstract type that is used to specify a behavior that classes must implement.
  - Is just a contract. The implementing class ensures, that it will have these methods that can be used on it. It is basically a contract or a promise the class has to make.
  - A class can implement multiple interfaces
- A Java interface is a bit like a class, except a Java interface can only contain method signatures and fields. An Java interface cannot contain an implementation of the methods, only the signature (name, parameters and exceptions) of the method.

- Interfaces cannot be instantiated (does not container constructor), but rather are implemented. A class that implements an interface must implement all of the non-default methods described in the interface, or be an abstract class.
- Object references in Java may be specified to be of an interface type; in each case, they must either be null, or be bound to an object that implements the interface.
- Interfaces can extend multiple interfaces

## Why use?

- Interfaces are the best way to maintain well decoupled constructs.
- You can use interfaces in Java as a way to achieve polymorphism.


## Override method

- annotation
  - Use of @Override above method declaration, to say it is using the method from the interface
- Why?
  - https://stackoverflow.com/questions/94361/when-do-you-use-javas-override-annotation-and-why
  - https://javarevisited.blogspot.com/2012/11/why-use-override-annotation-in-java.html

## Inheritence

- inherit from interfaces
  - classes
  - interfaces
- multiple inheritence

## Default Methods (JAVA8 +)

- Issues
  - Multiple inheritence

## other
- methods

- Reference types
  - polymorphism
  - cannot use concrete implementation class which has its own method with this ref type



## Links
