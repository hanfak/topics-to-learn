# 1. Single Responsibility Principle

- Any given component (class/function/module) should do one well-defined thing, and only that one well-defined thing.
- A component should have only one reason to change
- if a class has more than one responsibility, it will have to change whenever any one of its many responsibilities change.
- In the short term, it may be easier to simply keep adding methods to an existing class, regardless if the new functionality is within the responsibility of the class or not.
  - LLater, you will notice that your classes become large and closely coupled with each other
  - the size of each class will make it hard to fully understand its behavior and its role
  -
- Why?
  -  A component that conforms to SRP only needs to be changed when the thing it is responsible for changes
  - Each class now has fewer lines of more highl related code,so it should be easier for a developer to understand in its entirety
  - More individual source code files (one for each responsible class) should result in fewer merge conflicts
  - Testability is likely to be better and the related test code more highly focussed and cohesive
  - reduce the complexity of your code
  - makes it easier to refactor, reuse
- Promoting Single Responsibility
  - guidelines
    - Keep class length below two to four screens of code
    - Ensure that a class depends on no more than five other interfaces/classes.
    - Ensure that a class has a specific goal/purpose.
    - Summarize the responsibility of the class in a single sentence and put it in a comment on top of the class name. If you find it hard to summarize the class responsibility, it usually means that your class does more than one thing.
  - Breaking guidelines means you need to refactor
  - higher level of abstraction
    - you should partition your functionality across modules to avoid overlaps
    - try to summarize responsibility of a module or an application in one or two sentences
    -  Limit its scope and isolate it from the rest of the system using an explicit interface 

## Links

- https://stackify.com/solid-design-principles/
- https://dzone.com/articles/solid-principles-single-responsibility-principle
