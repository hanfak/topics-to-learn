# Dependency Injections

## What

- A dependency references other classes to complete some work
  - delegate work to another class
  - send a message to another object from the calling class
    - Just calling an instance method of an object with or without arguments
- All classes have dependencies
- Dependencies are provided to a class instead of the class creating them
  - This happens at creation time
- the app has control and proactively injects the required objects.

### links

- https://www.techyourchance.com/dependency-injection-myths-debunked/
- http://www.bryancook.net/2011/08/on-dependency-injection-and-violating.html
- https://dzone.com/articles/about-dependency-injection
- https://completedeveloperpodcast.com/episode-185/
- goolge talk https://www.youtube.com/watch?v=o-ins1nvbDg&feature=youtu.be
- https://developer.android.com/training/dependency-injection#kotlin

## Why

- that reduces coupling and promotes the open-closed principle.
- provides references to objects that the class depends on, instead of allowing the class to gather the dependencies itself.
- it  is about knowing as little as possible.
  - SRP
- allows classes to “not know” how their dependencies are assembled, where they come from, or what actual implementations are fulfilling their contracts.
-  not using the “new” keyword in your classes and demanding instances of your dependencies to be provided to your class by its clients.
-  reduces local complexity of the class and makes it dumber, which is a good thing.
  - Without knowing who the provider of the contract is or how to get an instance of it, our class can focus on its single responsibility
  - reduce coupling
- requires less understanding of the rest of the system to modify and unit test the class
- By removing the assembly code from your classes, you make them more independent, reusable, and testable.
- Dependency inversion relies on this idea


## Constructor Injection

- pass the dependencies of a class to its constructor.


## Setter Injection
- dependencies are instantiated after the class is created.
- https://www.vojtechruzicka.com/field-dependency-injection-considered-harmful/

## Field Injection
