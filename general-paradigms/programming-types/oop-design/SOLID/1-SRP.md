# 1. Single Responsibility Principle

- Any given component (class/function/module) should do one well-defined thing, and only that one well-defined thing.
- A component should have only one reason to change
- if a class has more than one responsibility, it will have to change whenever any one of its many responsibilities change.
- Why?
  -  A component that conforms to SRP only needs to be changed when the thing it is responsible for changes
  - Each class now has fewer lines of more highl related code,so it should be easier for a developer to understand in its entirety
  - More individual source code files (one for each responsible class) should result in fewer merge conflicts
  - Testability is likely to be better and the related test code more highly focussed and cohesive

## Links

- https://stackify.com/solid-design-principles/
- https://dzone.com/articles/solid-principles-single-responsibility-principle
