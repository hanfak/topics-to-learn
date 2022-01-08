# Composition Root

- Let’s create a SINGLE top layer place to define how our application is composed
- It is like a Table of Contents or Index for a reference book. If I ask a non-critical-thinking java developer “should reference books have a ToC and/or index to find things?”
- Where should we compose object graphs?
  -  each class should require its dependencies through its constructor, but this pushes the responsibility of composing the classes with their dependencies to a third party.
  - As close as possible to the application's entry point.
    - This is the composition root
  - Rather than as close as possible to the
- A Composition Root is a (preferably) unique location in an application where modules are composed together.
  -  all the application code relies solely on Constructor Injection (or other injection patterns), but is never composed. Only at the entry point of the application is the entire object graph finally composed.
-  Only applications should have Composition Roots. Libraries and frameworks shouldn't.
-  A DI Container should only be referenced from the Composition Root. All other modules should have no reference to the container.
