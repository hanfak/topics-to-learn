# Dependency Injections

## What

- A technique that enables loose coupling
- collaborating classes should rely on infrastructure to provide necessary services
- A dependency references other classes to complete some work
  - delegate work to another class
  - send a message to another object from the calling class
    - Just calling an instance method of an object with or without arguments
- All classes can have dependencies, it is how they managed
- Dependencies are provided to a class instead of the class creating them
  - This happens at creation time called object composition in a composition root
- the app has control and proactively injects the required objects.
- Dependencies are not defined by the number of modules but the number of times each module depends on another module
- Manage dependency lifecycle 
- Allow for dependencies to be intercepted

### links

- https://www.techyourchance.com/dependency-injection-myths-debunked/
- http://www.bryancook.net/2011/08/on-dependency-injection-and-violating.html
- https://dzone.com/articles/about-dependency-injection
- https://completedeveloperpodcast.com/episode-185/
- goolge talk https://www.youtube.com/watch?v=o-ins1nvbDg&feature=youtu.be
- https://developer.android.com/training/dependency-injection#kotlin

## Issues 
- can be over reliant on frameworks or libraries to do this for you
  - pollute code with framework (reduced separation of concerns)
- Needs to start an app with DI at the beginning, otherwise it becomes harder later on
- can add more complexity

## Why

- Improves maintainability
- that reduces coupling and promotes the open-closed principle.
- provides references to objects that the class depends on, instead of allowing the class to gather the dependencies itself.
- it  is about knowing as little as possible.
  - SRP
- allows classes to “not know” how their dependencies are assembled, where they come from, or what actual implementations are fulfilling their contracts.
- not using the “new” keyword in your classes and demanding instances of your dependencies to be provided to your class by its clients.
- reduces local complexity of the class and makes it dumber, which is a good thing.
- Without knowing who the provider of the contract is or how to get an instance of it, our class can focus on its single responsibility
- reduce coupling
- requires less understanding of the rest of the system to modify and unit test the class
- By removing the assembly code from your classes, you make them more independent, reusable, and testable.
- Dependency inversion relies on this idea

### Relevant for late binding 
- late binding = ability to replace parts of an app with recompiling code
  - ie third party addons, or support different runtime env
- Can change the implementation of different database/algorithm, depending on env/settings/configuration/inputs
- This allows the decision to decide on what service to use as late as possible, to defer the choice 
  - then can use one service, but not tied to it, so can easily swap it out for another service with minimal changes
### Relevant for unit testing 
- Allows you to swap out injected dependencies with ones that can be controlled to setup situations for different test cases
### Type of Abstract factories
- Methods that create objects of certain kind 
- DI is not a service locator, or a service to call to get dependencies
- DI is a way to structure code so that you never have to imperatively ask for Dep 
### Does not require a DI Container 
- A DI container aim is to make it easier compose classes and wire up an application
  - it might add unnecessary  overhead for it to be worth using
  - it is an optional tool to implemetn DI
- Using DI without a container library is called PURE DI 
- Pure DI allows you implement DI without compromises 
  - might take a more work 
  - easier to follow
### Intercept dependencies 
- With DI, can intercept each dependency instance and act on it before it is passed to the consumer 
- Decorating 
- Allows for cross cutting concerns to be applied outside of the consumer
### Seams
- Is a place where an application is assembled from it's constituent parts 
- Where you can disassemble the application and work with the modules in isolation
- Use of interface, so that class relies on the interface rather than implementation
- allows you to handle volatile dependencies
### Managing volatile dependencies 
- dep that change or can change should be injected 
- Stable dependencies dont need to be injected 
  - Might be useful testability or other reasons
#### Stable Dependencies 
- Criteria 
  - The class/module already exists 
  - expectation that new versions won't contain breaking changes
  - The types in question contain deterministic algorithms 
  - never expect to have to do the following with another class
    - replace
    - wrap
    - decorate
    - intercept the class/module 
  - specialised libraries that encapsulate algorithms relevant to your app
- stable if they are not volatile

#### Volatile Dependencies 

- Dependencies that don't provide a sufficient foundation for apps
- You introduce seams in your code to inject volatile dependencies
- Criteria
  - The dep introduces a requirement to set up and configure a runtime env for an app 
    - ie databases, out of process resources like message queues, webservices, filesystems
    - leads to lack of late binding, extensibility, testing
  - The dep does not yet exist or is still in development 
  - The dep isn't installed on all machines in the dev organisation
    - ie paid for 3rd party libraries, dep that cannot be installed on all OS
    - leads to disabled testability
  - The dep contains non deterministic behaviour 
    - ie randomness, time/date 
    - leads to hard to control behaiour for testing 

## DI Scope 

- As the class has no control of managing it's dep in DI, it has no control of the lifetime (when it goes out of scope, when it is created/reused) of the object injected
  - Does not know when it is created or goes out of scope
  - This simplifies the consumer 
- Thus the composition root can control the lifecycle of a dependency/objects/instances  
- Depending on your language you dont have to worry about the object scope, as this is handled by garbage collector
  - When no class references the dependency it is eligible for garbage collection
- In application, multiple consumers might use the same dependency
  - You can either inject a separate instance into each consumer
  - or you can choose to share a single instance across multiple consumers

## Intercepting Dependencies 
- DI allows the power to modify dependencies before passing them on to the consumer 
- Form of decorator pattern
- This is related to AOP (aspect oriented programming)
- can apply logging, auditing, access control, validation etc, to maintain separation of control

## Composition Root 
- Describes where and how you should compose an application's object graphs
  - where the object graphs performs the actual work of the app
- it is a single logical location
- Object graphs are composed as close as possible to the application's entry point
  - especially for loosely coupled classes 
- This can be 
  - Main method 
  - it can span multiple classes and then called in main method or via DI container
- Using constructor injection, pushes the responsibility for the creation of their  dependencies up to the consumer, which also pushes the consumer's dep to their consumers.
- Should be the only place where you use a DI container
  - Otherwise leads to service locator pattern (anit pattern)
- composition root should be in one module
- It is not part of the UI layer

### How it works 

- Acts as a third party that connects consumers with their services 
- Deferring the decision on how to connect the classes the more options you have 
- They are not reused
- All classes should use constructor injection (possibly others for good reasons)
  - this allows CR to decide how to compose the objects
- Should be only place that knows the structure of the object graphs
  - centralises the knowledge 
  - avoids application code passing on dependencies to other threads the run parallel to the current operation
    - as the consumer has no way of knowing if it is safe to do so
  - It is up to CR to create the object graph for each concurrent operation
- The CR relies on config/setting/property files
  - increases flexibility 
  - Should separate the loading of the config files to values, from the methods that does the object composition

### Avoid 
- Dont create the object graphs in many different locations
- This limits you from intercepting the object graphs to modify their behaviour (ie for testing replace a db with map)
- It is not part of the UI layer, although it is easiest to create composition root here
  - can take out the layer as module, but might be tricky

### DI containers 

- software library that can automate many tasks for composing objects and managing lifetimes 
- should only be used to compose object graphs
- Only be in the composition root
  - CR should have reference to DI container
  - DICon should not be referenced by any other module
- removal of any coupling between the DI container and app code base
- For request based applicatoins (websites/services)
  - you configure the container once, but resolve an object graph for each incoming request

## Constructor Injection

- allows a class to statically declare its required dependencies
- To guarantee a necessary volatile dependency is always available to the class, by requiring all callers to supply this dependency as a parameter to the class's constructor
- pass the dependencies of a class to its constructor as parameters, thus store the reference for future use
- The composition root will supply these dependencies, by instantiating them and injecting them
- Should be default choice for DI

### How it works
- The class that needs the dep, needs to expose a constructor 
  - This can also be done via static factory method
- The dependency passed in to constructor should be assigned to a field
  - This allows the field (dep) to be used anywhere in the class
  - Generally, the field will be of an abstract type (depends on the patterns used)
- The field holding the dependency should be read only (no setters)
  - Thus after object instantiation, the dependency cannot be modified
- There should be no other logic in the constructor (see below exception for validation)
- Dep injected into a class are few, but the depth of the object graphs might be long/deeper, due to the multiple layers of decorators
  - Have large parameter lists for constructors, can have an adverse effect on performance 

### Benefits 

- Clearly documents what the class requires via it's constructor parameters
- Makes sure the class cannot create an object if it has not been passed a dependency that it needs to function
  - injection guaranteed

### Bad 

- Some frameworks need to break this implementation to work
- Some frameworks may need you to have a parameterless constructor (hibernate, ant)
  - leading to more work and configuration to setup properly

### Multiple constructors 

- There are patterns which allow a class to have multiple constructors (Via telescoping) that allows defaults 
  - This can allow a class to have constructors with more or less parameters than previous constructor
  - These can be helpful, especially in refactoring a class for testing 
  - This can lead to ambiguity in terms of which constructor should be called or DI Con should use 
- Alternatively, can have one constructor, and have multiple explicitly named static factories which call the constructor
- For application constructors having one constructor is preference, while in libraries having multiple is preferred

#### Optional dependencies 

- This can be a consequence of having multiple constructors 
- They can complicate checks for null arguments 
- Give greater flexibility in constructing a specific object
- Best to use the builder or factory patterns
- Can maintain a single constructor, but the composition root can inject a `null object` which has no behaviour
  - but code that uses this dependency must be careful of it's usage if it relies on a return type (output)
  
### Validating constructor arguments 

- This is doing guard clauses to make sure that args are correct before constructing the object 
  - So that when the dep is used elsewhere in the class no issues with null pointer
- Two camps, one saying constructors should just be purely for assigning the reference for the dependecy to the class, and others saying should assign validation 
- I believe they should be pure with no validation, and create static factories that will do the validation before instantiating the object 
  - Not all classes should need validation, only those at the edge of the system, or can be constructed at runtime (without the coders knowledge - but for to reduce failure might better to have default dependency instead of throwing an exception)
  - This might lead to issues with DI Con frameworks from not easily using it, with extra work to create (ie @bean and @configuration in Sprin)

## Setter/Method Injection

- Enables you to provide a dependency to a consumer when either the dependency or the consumer might change for each operation
  - Dependency can vary with each method call
  - Consumer of such dependency can vary on each call
- dependencies are instantiated after the class is created.
- Dep supplied with method parameter
- Done outside of composition root

### Good 

- Allows caller to provide operation specific context or service
- Allows inject dep into data centric objects that are not created inside composition root

### Bad 

- limited applicability
- causes the dep to become part of the public api of a class or it's abstraction

### When 

- Creating entities (DDD)
  - due to entities possibly containing lots of methods, these will require only certain dependencies
  - yes, can inject all dep via constructor, but not all will be used within each method
    - which complicates testing

### Avoid 

- Dont store the dependnecy when passed in via method args 
  - leads to temporal coupling, captive dependencies, hidden side effects
  - just use it or pass it on

## Field/Property Injection
- By exposing a writable property/field, that lets the caller supply a dep, if they want to override the default (one created in constructor)
- having a public non final field, where you can inject the dependencies
- dependencies are instantiated after the class is created

### Good 

- Allow for class to be extensible
### Issues 
- NPE
  - object created may have null fields, as they dont need to be assigned when object is instantiated
  - CURE: Have a default at constructor time
- Causes temporal coupling
  - lead to inconsistent behaviour
- Hard to impl in robust manner
- https://www.vojtechruzicka.com/field-dependency-injection-considered-harmful/

### when 

- when you have a good local default but want to extend by allowing users to provide diff impl
- only applicable to resuable libraries
  - allows components to define sensible defaults
- Dont use for applications


## Issues with injecting too many dependencies

- Some times having too many dependencies injected, can make the code more complex (esp for testing)
- Things like crosscutting concerns (logging, date etc) can pollute the class.
  - Instead try using a factory, which can pass a supplier to a static factory method, and when the method of dependency is called, can call the supplier and instantiate it. Then the supplier is passed in at composition root, or a stub/fake is passed in for tests
- https://enterprisecraftsmanship.com/posts/singleton-vs-dependency-injection/

## DI anti patterns 

### Service locator 
### Control freak 
### Ambient Context
### Constrained Constructor

## Code smells 

### constructor over injection
### abstract factories abuse 
### cyclic dependencies

## Object lifetime 
### Singleton 
### Transient 
### Scoped 

## interception
### Decorator 
### cross cutting