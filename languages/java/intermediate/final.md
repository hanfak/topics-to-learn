# Final

- final fields or variables cannot bereassigned
  - Used to create constants
  - or fields that can only be defined via constructors at the time of object instantiation
  - As the reference is stored in the field/variable, it's object graph (internal fields) can be accessed
    - thus they can be change if the fields of the original field is mutable (ie via public field or getter)
  - This does not mean that the fields are immutable
  - Part of making class immutable if fields are final
    - but must make sure that the object graph is also immutable
  - any final field must be initialized before the constructor completes.
    - static final fields, this means that we can initialize them:
      - upon declaration as shown in the above example
      - in the static initializer block
    - For instance final fields, this means that we can initialize them:
      - upon declaration
      - in the instance initializer block
      - in the constructor
- Final arguments can’t be changed inside a method
- final methods cannot be overriden by subclasses
  - you’d mark a method as final when you’re defining a parent class and want to guarantee certain behavior of a method in the parent class, regardless of which child is invoking the method.
- final classes cannot be subclassed/extended
  - prevents a user extending a class and replacing it with a subclass which might give access to private state or non private behaviour, which could be used during runtime.
- What’s the difference between making all methods of the class final and marking the class itself final?
  - In the first case, we can extend the class and add new methods to it.
  - In the second case, we can’t do this.
- Good practice to use final everywhere
  - Depends, as it can lead to a lot of verbose code
  - As long as you code with the convention of all method param, local variables as final

## Links

- https://www.baeldung.com/java-final
- https://www.geeksforgeeks.org/final-keyword-java/
