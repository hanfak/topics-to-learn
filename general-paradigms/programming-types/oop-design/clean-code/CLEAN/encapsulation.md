# Encapsulation

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Encapsulation](#encapsulation)
	- [Definitions](#definitions)
	- [Benefits](#benefits)
	- [Information hiding](#information-hiding)
	- [Encapsulation is not information hiding](#encapsulation-is-not-information-hiding)
	- [Breaking encapsulation](#breaking-encapsulation)
	- [Encapsulation and frameworks](#encapsulation-and-frameworks)

<!-- /TOC -->

- Encapsulation is a programming language feature.

## Definitions

- Encapasulation is making something which is varying appear to the outside as if it is not varying.
- Encapsulation allows us to tame the growing state and complexity
  - The idea that we can internalize the state, hide it from other components, and offer only a carefully designed API surface for any state mutation is core to the design and coding of complex information systems
- Encapsulation means drawing a boundary around something. It means being able to talk about the inside and the outside of it
- What can be encapsulated
  - Relationships
  - processes
  - varying behaviours
  - the number of steps
  - the order of steps in a process
  - hide a concept behind an abstraction/interface
  - hide the way you implement an algorithm behind a method signature
  - Wrap foreign code in your code via adapter/facade pattern
- an object being strongly or weakly encapsulated depending on how much of its implementation is hidden.
- done via, "program to an interface not an implementation"
- What you don't know can't hurt you
  - Encapsulate by policy, reveal by need
  - Make everything private, then expose more ie package, protected or public, to expose later
- Encapsulation allows you to check access to your own innards, and provide specific methods of performing such access
  -  It does not specifically address leaking implementation details; although you can control access to that variable, you can no longer control the fact that the client knows your using an ArrayList, even if you later decide to use LinkedList.
- Encapsulation is the grouping of related ideas into one unit, which can thereafter be referred to by a single name.
  - attributes that represents the state of an object and the methods that work on them are packaged into an object type.
  - Putting the responsibility for each object with the object itself where it belongs
- The result of hiding a representation and implementation in an object...
- Encapsulation is an OOP concept where object state(class fields) and it's behaviour(methods) is wrapped together. Java provides encapsulation using class.
- Quality code occurs when it hides the implementation details form the rest of the world.
- Not just making state or behaviour private
- Aim to **to hide the interface (what I am trying to accomplish) from the implementation (how I accomplish it)**
- Comes from designing **outside in* and not **inside out**
  - Need both, to see the big picture
- The domain model should be separate from implementation details as possible
- We want to model things in the world we also want to model their limited perspective
- All about delegating to other objects to do the work
- Design patterns encapsulate something differently
- Manages complexity, keep the caller out of the implementation details of the callee, makes it easier to change
  - If my tests are implementation dependent, I have encapsulation issues


## Benefits

- The more you can hide how you implement something, the more freedom you have to change the implementation later without affecting other parts of the code
- Keeps code more modular and simpler to work with
- What you can hide, you can change later without breaking other code that depends on it
- Reduce ripple effect
- if you dont know about something you can't couple to it.
  - Fewer dependencies make code easier to change
- Prevent hard bugs to solve caused by inconsistent state

## Information hiding

- Information Hiding is a design principle
  - use interfaces rather than objects (other than at creation).
- information hiding gives rise to the notions of encapsulation and abstraction.
- every module in the [...] decomposition is characterized by its knowledge of a design decision which it hides from all others. Its interface or definition was chosen to reveal as little as possible about its inner workings.
  - some separate entity or module which has some responsibility that we need fulfilled, and we are not interested about how it is fulfilled. But the emphasis here is a bit more about hiding the details from other modules (or objects)
- InformationHiding is the idea that a design decision should be hidden from the rest of the system to prevent unintended coupling
- is hiding the fact that your using an ArrayList to implement your data structure. Although the client could still find out how your implementing it (Information Hiding Is Not Information Erasing), you're no longer responsible for supporting that implementation.
- mechanism for restricting access to some of the object's components. Your above example is the case of Information Hiding if you make age private.
- Information hiding is a great principle for enabling focus on a useful abstraction rather than a mass of detail, for sure. But it implies a choice to delve into details only when relevant, not ignorance of the details.

## Encapsulation is not information hiding

- Information Hiding should inform the way you encapsulate things, but of course it doesn't have to
- encapsulation does need some degree of information hiding.

- https://www.javaworld.com/article/2075271/core-java/encapsulation-is-not-information-hiding.html
- http://web.archive.org/web/20000816234125/http://www.itmweb.com:80/essay550.htm
- http://web.archive.org/web/20090505194203/http://homepage.mac.com/keithray/blog/2006/02/22/#EncapsulationHiding
- http://wiki.c2.com/?EncapsulationIsNotInformationHiding
- http://www.stefanoricciardi.com/2009/12/06/encapsulation-and-information-hiding/

## Breaking encapsulation

- Examples
  - Using setters
  - violating law of Demetar
  - using the details of impl of an object, rather than a cleaner interface
  - not using interface
  - non final fields
  - data structures that can be mutated despite reference to it
  - use of reflection
  - inheritance
  - patterns like visitor
  - Using the toString output, to get values of fields

## Encapsulation and frameworks

- Frameworks dont work well with immutability.
  - They need fields to be non final, or setters need to be created
-  use an anticorruption layer to protect and validate your internal state after those setter interactions

## Drawbacks

- you protect "mutable" state within the object with methods that receive messages and these public interface methods would protect data -- especially if you are working with multi-threaded applications
	- This allowed us to limit the scope of the code that had access to mutate the data.
	- this did not get rid of the problems with working with multi threaded applications, just reduced it to one area
	- The lack of good coding standards and frameworks, has led to code breaking encapsulation
	- Since the data is mutable and the functions and methods mutate the data and rely on the state which can change - testing the correctness of any algorithmic function is meaningless in the overall correctness of the object or the application.
	- To avoid the issues with mulit threading, we need to synchronize the data access in the object itself which is often not done perfectly.
- The move to immutable data, means no changes to data/state in the class, thus encapsulation is just a grouping of functions in such classes
