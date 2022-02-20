# Loose Coupling

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Loose Coupling](#loose-coupling)
	- [Promoting Loose Coupling](#promoting-loose-coupling)
	- [Avoiding Unnecessary Coupling](#avoiding-unnecessary-coupling)
	- [Models of Loose Coupling](#models-of-loose-coupling)

<!-- /TOC -->

- keep coupling between parts of your system as low as necessary
- Loose coupling refers to a situation where different components know as little as necessary about each other
- Allows to scale system
- High coupling means that changing a single piece of code requires you to inspect in detail multiple parts of the system
  - The higher the overall coupling, the more unexpected the dependencies and higher chance of introducing bugs.
  -  Low coupling would allow you to introduce these changes without the risk of breaking other parts of the system.
- Low coupling promotes keeping complexity localized.
  - In a low coupled system, multiple engineers can work on them independently
  - you will be able to scale your company by hiring more engineers, since no one has to know the entire system in full detail to make “local” changes
- Decoupling on a higher level can mean having multiple applications, with each one focused on a narrow functionality
  - You can then scale each application separately depending on its needs
    - ie some parts may need more processors, others need more memory
  - Provide hardware to meet the requirements of each part of the system easily, with out using excess
	-  is to reduce the assumptions two parties (components, applications, services, programs, users) make about each other when they exchange information. The more assumptions two parties make about each other and the common protocol, the more efficient the communication can be, but the less tolerant the solution is of interruptions or changes because the parties are tightly coupled to each other

## Promoting Loose Coupling

- Need to carefully manage your dependencies.
- **A system is the whole—it contains everything: all of the applications you develop and all the software you use in your environments.**
  - Applications are the highest level of abstraction within the system, and they serve highest-level functions
- Within an application you have one or more modules that implement finer, more granular features.
  - modules should be independent enough for multiple teams to work on them in parallel
  - They can be deployed independently
- your modules consist of classes, which are the smallest units of abstraction.
  - A class should have a single purpose and no more than a few screens of code
- ou can promote low coupling by correct use of public, protected, and private keywords
  - You want to declare as many methods as private/protected as possible.
  - more methods you make private, the more logic remains hidden
  - The less access other classes have to your class, the less aware they are of how the class does its job.
  - Private methods can be refactored and modified easily, as you know that they can only be called by the same class.
    - the complexity is localized and you do not have to search far to find out what could potentially break
  -  Once a method is public, you cannot assume that no one is using it anymore and you have to search carefully throughout the application
    - esp if making any changes
- you want to reduce the contact surface area between parts of your system
  - Loose coupling should let you replace or refactor each element of the system without major work on the rest ofthe system.
  - Need to find the balance between decoupling and overengineering
  - the contact surface area is determined by the number of dependencies that cross boundaries of two elements of your diagram
  - Remove cyclic dependencies between entities
- Use interfaces, and dependent entites use these instead of the implementations
  - keeps contract safe
  - allows changes in implementation, or swap out what implementation to use at runtime

## Avoiding Unnecessary Coupling

- Don't all the private properties/fields using public getters and setters.
  - this might not be possible due to using certain libraries
  - Better to start with private methods and make them protected or public only when really necessary
    - Even better, make the objects immutable
- Dont let clients of a module or class need to invoke methods in a particular order for the work to be done correctly
  - The client knows to much
  - Clients should be able to use the public interface in any way they want
- Dont allow circular dependencies between layers of your application,modules, or classes
  - Draw diagrams
  - A diagram of a well-designed module should look more like a tree (directed acyclic graph) rather than a social network graph

## Models of Loose Coupling

- A good example of loose coupling is the design of Unix command-line programs and their use of pipes
- SL4J logging framework for java
  - A good example of loose coupling is the design of Unix command-line programs and their use of pipes
  -

## Tight Coupling

- Example
	-  a local method invocation.
	- Invoking a local method inside an application is based on a lot of assumptions between the called and the calling routine.
	- Both methods have to run in the same process (e.g. a virtual machine) and be written in the same language (or at least use a common intermediate language or byte code).
	- The calling method has to pass the exact number of expected parameters, each using the correct type.
	- The call is immediate, i.e. the called method starts processing immediately after the calling method makes the call.
	- Meanwhile, the calling method will only resume processing when the called method completes (meaning the invocation is synchronous).
	- Processing will automatically resume in the calling method with the next statement after the method call.
	- The communication between the methods is immediate and instantaneous, so neither the caller nor the called method have to worry about security in the form of eavesdropping 3rd parties.
	- All these assumptions make it very easy to write well structured applications that break functionality into individual methods to be called by other methods.
	-  A large number of small method allow for flexibility and reuse.
