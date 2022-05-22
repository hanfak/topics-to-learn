# 1. Single Responsibility Principle

- Any given component (class/function/module) should do one well-defined thing, and only that one well-defined thing.
- A component should have only one reason to change
- if a class has more than one responsibility, it will have to change whenever any one of its many responsibilities change.
- In the short term, it may be easier to simply keep adding methods to an existing class, regardless if the new functionality is within the responsibility of the class or not.
  - LLater, you will notice that your classes become large and closely coupled with each other
  - the size of each class will make it hard to fully understand its behavior and its role
  -

## Why?
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


## Separation of concerns

- SRP is known as this
- Anything with "and" when describing the actions of the behaviour/method one should think of separating out
- Separating concerns, improves modularity and composability
- Be careful implicit behaviour
  ```java
  assertThat(Fractions.addFraction("1/3", "1/3")).isEqualsTo("2/3");
  ```
  - This is only adding fractions from the name, but is doing a lot more
    - The behavior is doing taking two strings, parses them, and calculates their sum.
  - It should just calculate the sum and nothing else
  - Instead
  ```java
  Fraction fraction = new Fraction(1, 3);
  assertThat(fraction.addFraction(new Fraction(1, 3))).isEqualsTo(new Fraction(2, 3));
  ```
## Issues

- This can lead to many small classes, with logic split all over the place.
  - Leads to lots of coupling between lots of objects
  - Hard to understand the flow of the logic, this can lead to hard to debug
- Having one module that can be used by many consumers, leads to good reuse, but high coupling
  - So if one consumer needs to change this shared module, this can affect all the other consumers that use this shared module.
  - This can happen when applying SRP wrongly
  - Instead the shared module should bot shared across domain boundaries
- Better to call it **Single Concept Responsibility**
  - A module should represent a single concept
- It can be too focused on size of the module
- It is very vague, thus different opinions
- IF it is about pure functions, then it makes sense due to the definition of functions
  - but applied to objects, where state is exists, its harder to apply to
- https://naildrivin5.com/blog/2019/11/11/solid-is-not-solid-rexamining-the-single-responsibility-principle.html

## Links

- https://stackify.com/solid-design-principles/
- https://dzone.com/articles/solid-principles-single-responsibility-principle
