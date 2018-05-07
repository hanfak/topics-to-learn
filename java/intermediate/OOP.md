# Object Oriented Programming

## Object creation

- https://self-learning-java-tutorial.blogspot.co.uk/2014/02/object-creation-and-destruction.html
-
## links

- https://www.thesoftwareguild.com/blog/object-oriented-programming/

## Constructors

### Default/hidden constructor
### Overlaoding
### Private constructors
### Telescoping
### Static initialization

## Fields/state

- static final
- final
- static variables

### Accessors and variable scope

- variable scope is where the variable is accesible
- parameters and variables declared in method are only avialable in that method.
  - when method ends, the reference of the variable goes away and cannot be accessed again
- instance fields are avialable in any instance method in the class
  - accessors does not affect this
  - stays in scope until the object is deleted (garbage collector)
- static variables are avialable
  - only defined in class not method
  - shared among all instances of any class.
  - not thread safe, must be made final
  - stays in scope until program ends
- loop scope
  - where a variable is declared in the loop ie for loop, and is thus only accessed in the loop.
- block scope
  - variable declared in block, ie if block, can only be used in that block, when block finishes it is destroyed.

- This
  - Example:
```java
private String username;

public void changeUsername(String newName) {
  this.username = newName;
}
```
  - Conflicting local variable and class variable has the same name.
  - this prevents conflicts
  - this refers to the class variable


- Public
- Package protected (default)
- protected
- private

## Methods/behaviour

### Instance Methods

- Creating
- Calling

### Class/Static Methods

- Creating
- Calling

### Static VS Instance

### Method variables (local variables)

## Variable scope

## Pass by reference

## Object equality


## Nested Classes
- member inner Class
- local inner class
- annonymous inner Class
- static nested class

## Interfaces (new file)
- methods
- overide method
  - annotation
- inherit from interfaces
- Reference types
  - polymorphism
  - cannot use concrete implementation class which has its own method with this ref type
- multiple inheritence
- Default methods
  - multiple inheritence issue


## Inheritence (new file)
- abstract class
  - abstract method
  - extending
  - difference with interface
- super Class
- sub class
- super
- No multiple inheritence
- use of final

## Links
