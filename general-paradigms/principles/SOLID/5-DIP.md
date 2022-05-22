# 5. Dependency Inversion Principle

-  reduce tight coupling
- The first that higher level code should not depend on lower level code, instead both high and low level code should depend on some abstraction
- the abstractions should not depend on the details, rather the other way around, that the details should depend on the abstractions.
- higher level code here represents the “what” or “workflow” with the lower level code performing specific actions as part of this workflow.
- Can use different implementations of the dependency
- DIP in conjunction with dependency injection also makes it possible to provide different concrete implementations of dependencies at runtime.

Why?
- Without DIP, the high level “workflow” is harder to separate from the implementation (in the lower level code).
- Classes are more tightly coupled, meaning that changes can ripple throughout the system
- it may make unit testing harder because fake versions of dependencies cannot easily be supplied
  - As newing objects occurs in the class under test

## Issues

- This is all about adding flexibility, codeing to the an interface
  - Taken to the extreme is bad
- This came about due to mocking frameworks needed interfaces, to be able to mock
  - Then adding final to the class, meant you could not mock it
- With all this dependency injection, you need a class/s in layer, that knows about all these dependenices, to be able to construct the object map
  - frameworks used to use xml config, now they use annotations, which make the code hard to follow

### Links
  - https://naildrivin5.com/blog/2019/12/02/dependency-inversion-principle-is-a-tradeoff.html

## Links

- https://dzone.com/articles/solid-design-principles-explained-dependency-inver
- https://dzone.com/articles/solid-principles-dependency-inversion-principle
- https://stackify.com/dependency-inversion-principle/
