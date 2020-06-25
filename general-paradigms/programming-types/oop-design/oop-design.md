## OOP Design

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

	- [OOP Design](#oop-design)
	- [Use of diagramming and planning](#use-of-diagramming-and-planning)
	- [OO features](#oo-features)
	- [Design Principles](#design-principles)
		- [Links](#links)
	- [SOLID Principles](#solid-principles)
		- [Links and Books](#links-and-books)
	- [links](#links)

<!-- /TOC -->

Writing a program to do something is the first and easy part, writing it and change it (refactoring it) with good design and knowing the trade offs is different.

The only constant in application is change. That is why the soft is in software. To make change easy/fast/efficient/cheap we need software to be designed with this in mind. Software design helps with making the software more readable/maintainable/extendable with out increasing costs or time for reading/maintaining/extending.

a lot of what writing good code is about comes down to making proper use of abstraction levels, and deciding which abstractions to put in place is the first step to a good design.

Improving OO design or any software design is to keep software soft.
  - why?
    - May result in lower total cost of ownership (TCO) for a longer-lived system
    - May allow the business to be more agile (responding more quickly to changing marketplace conditions)
    - May result in happier development teams (which in turn,may increase productivity and reduce staff turnover)

ultimately it is the code that must be transformed from its current state to a new state to support the goals of the organisation or users.


## Use of diagramming and planning

- UML
  - Sequence diagrams
    - Big picture - full process of an application
    - single flow
- Architectrual diagrams
  - team apps including 3rd party/ database/ filesystems
  - full service - all apps that provide all the services


## OO features

Using an OO programming language does not mean that you are programming in a OO style. Sometimes you will use a procedural style. Knowing the features and using them will help in taking advantage of the benefits of OO.

- Polymorpshism
- Encapsulation
- Abstraction
- inheritence

- Object-oriented programming, there’s basically three main concepts.
	- There are objects, which hold state and accept messages,
	- there are the messages that are sent between objects, and
	- there are the methods, which are the code that runs when the message is received.
- In this way, you create this network of objects that communicate with each other. The computation happens through the dispatch of different messages and what each object does with the messages it receives
- https://stackify.com/oops-concepts-in-java/

## Design Principles

Implementing these design principles to have better code

- Use SOLID principles (See below)
- high cohesion
- low coupling
- separation of concerns
- YAGNI
- DRY
  - Avoid Duplication
- Tell, dont ask
- law of demeter
- dependency injection
- composition over inheritence
- code to interface
- inversion of control
- Let the compiler pick up on errors
  - use Generics
- Anything from effective java
- Comment on the why, not the why
- Compose method with other methods

### Links

- https://jelastic.com/blog/10-object-oriented-design-principles-java-programmer-should-know-guest-post/
- http://javarevisited.blogspot.co.uk/2012/03/10-object-oriented-design-principles.html
- [Core Design Principles for Software Developers by Venkat Subramaniam](https://www.youtube.com/watch?v=llGgO74uXMI&t=2s)
- https://dzone.com/articles/software-design-principles
- https://dev.to/racingdeveloper/from-procedural-to-objects-applying-the-tell-dont-ask-principle

## SOLID Principles

- SRP - Single Responsibility Principle
- OCP -  Open Closed PRincple
- LSP - Liskov Substitution Pricinple
- ISP - Interface Segregation Principle
- DIP - Dependency Inversion Principle

### Links and Books

- https://github.com/mikeknep/SOLID
- http://williamdurand.fr/2013/07/30/from-stupid-to-solid-code/
- https://dev.to/naveen/how-to-write-an-object-oriented-program-that-doesnt-suck
- https://dzone.com/articles/object-oriented-programming-concepts-with-a-system

## links

- http://blog.thecodewhisperer.com/permalink/putting-an-age-old-battle-to-rest
- https://www.tonymarston.net/php-mysql/oop-for-heretics.html#definitions
- https://tomassetti.me/oops-concepts/
- https://medium.com/@richardeng/a-simple-explanation-of-oop-46a156581214
