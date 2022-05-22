# Habitability

- Habitability is the characteristic of source code that enables [people] to understand its construction and intentions and to change it comfortably and confidently.
- There is a clear structure
- future proof software
- It’s easy to start working with and the accompanying documentation is clear and self-maintaining.
- provides joy and ease to work with
- CUPID aims  to get your software this characteristic
- Code base can become habitable,
  - through refactoring
  - through broken glass theory, code is in good condition then we will keep it that way
  - Have a consistent style throughout the codebase, which we aim to maintain
  - We get credit for making our code simple and easy to understand. We get credit for loose coupling, for testability, for shallow hierarchies, for good exception handling, for fluid interfaces, for not giving our co-workers headaches, essentially for all around good design.
- To see if you have habitable code
  - How easy is it for them to come back to?
  - How easy is it for others to work with their code?
  - How easy is it to follow?
  - How easy is it to understand at a quick glance?
- Overly complex code doesn’t make for habitable code.
  - often a waste of time using overly complicated solutions to optimise code, because modern compilers will be working hard to optimise it anyway
- How to get there
  - Stick to agreed conventions. Consistency helps make it easier to work in the code—ensure developers have access to a coding style document and are provided coaching on style
    - Enforce in code reviews, CI tests, static analysis tests, auto formatting in IDE
  - Use clear names of variables and functions
  - To be verbose and not be afraid of it (especially with function names).
  - Aim to write code that can be understood without any comments
  - But if a comment would make something clearer then add a comment. If there is a genuine chance something in the code is going to be misunderstood, regardless of the other steps taken: add a comment.
  - Use test names that explain what is actually being tested
    - makes it easier to investigate why a test is failing. Not only does it give a clearer indication of the test that’s failing, but it also shows what behaviour is meant to be happening in the first place. So, it helps cut down the time taken to investigate a failing test.
  - Write so a novice programmer could understand what is happening.

  ## Links

  - https://malvasiabianca.org/archives/2010/04/habitable-software/
