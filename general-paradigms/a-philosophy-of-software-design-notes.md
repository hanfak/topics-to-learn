# a-philosophy-of-software-design-notes

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [a-philosophy-of-software-design-notes](#a-philosophy-of-software-design-notes)
	- [From you tube talk](#from-you-tube-talk)
	- [Summary](#summary)
	- [Nature of complexity](#nature-of-complexity)
	- [Working code is not enough](#working-code-is-not-enough)
	- [Modules should be deep](#modules-should-be-deep)
	- [Information Hiding](#information-hiding)
	- [General purpose modules are deeper](#general-purpose-modules-are-deeper)
	- [Different layer, different abstraction](#different-layer-different-abstraction)
	- [Pull complexity downwards](#pull-complexity-downwards)
	- [Better together or better appart](#better-together-or-better-appart)
	- [Define Errors out of existence](#define-errors-out-of-existence)

<!-- /TOC -->

- https://tigerabrodi.blog/a-philosophy-of-software-design
- https://lethain.com/notes-philosophy-software-design/

## Summary

- Red flags
- 𝗦𝗵𝗮𝗹𝗹𝗼𝘄 𝗺𝗼𝗱𝘂𝗹𝗲: the interface for a class or method isn't much more straightforward than the implementation
- 𝗜𝗻𝗳𝗼𝗿𝗺𝗮𝘁𝗶𝗼𝗻 𝗹𝗲𝗮𝗸𝗮𝗴𝗲: a design decision is reflected in multiple modules
- 𝗧𝗲𝗺𝗽𝗼𝗿𝗮𝗹 𝗱𝗲𝗰𝗼𝗺𝗽𝗼𝘀𝗶𝘁𝗶𝗼𝗻: the code structure is based on the order in which operations are executed, not on information hiding
- 𝗢𝘃𝗲𝗿𝗲𝘅𝗽𝗼𝘀𝘂𝗿𝗲: An API forces callers to be aware of rarely used features to use commonly used features
- 𝗣𝗮𝘀𝘀-𝘁𝗵𝗿𝗼𝘂𝗴𝗵 𝗺𝗲𝘁𝗵𝗼𝗱: a method does almost nothing except pass its arguments to another method with a similar signature
- 𝗥𝗲𝗽𝗲𝘁𝗶𝘁𝗶𝗼𝗻: a nontrivial piece of code is repeated over and over
- 𝗦𝗽𝗲𝗰𝗶𝗮𝗹-𝗴𝗲𝗻𝗲𝗿𝗮𝗹 𝗺𝗶𝘅𝘁𝘂𝗿𝗲: special-purpose code is not cleanly separated from general-purpose code
- 𝗖𝗼𝗻𝗷𝗼𝗶𝗻𝗲𝗱 𝗺𝗲𝘁𝗵𝗼𝗱𝘀: two methods have so many dependencies that it's hard to understand the implementation of one without understanding the implementation of the other
- 𝗖𝗼𝗺𝗺𝗲𝗻𝘁 𝗿𝗲𝗽𝗲𝗮𝘁𝘀 𝗰𝗼𝗱𝗲: all of the information in a comment is immediately obvious from the code next to the comment
- 𝗜𝗺𝗽𝗹𝗲𝗺𝗲𝗻𝘁𝗮𝘁𝗶𝗼𝗻 𝗱𝗼𝗰𝘂𝗺𝗲𝗻𝘁𝗮𝘁𝗶𝗼𝗻 𝗰𝗼𝗻𝘁𝗮𝗺𝗶𝗻𝗮𝘁𝗲𝘀 𝗶𝗻𝘁𝗲𝗿𝗳𝗮𝗰𝗲: an interface comment describes implementation details not needed by users of the thing being documented
- 𝗩𝗮𝗴𝘂𝗲 𝗻𝗮𝗺𝗲: the name of a variable or method is so imprecise that it doesn't convey much useful information
- 𝗛𝗮𝗿𝗱 𝘁𝗼 𝗽𝗶𝗰𝗸 𝗮 𝗻𝗮𝗺𝗲: it isn't easy to come up with a precise and intuitive name for an entity
- 𝗛𝗮𝗿𝗱 𝘁𝗼 𝗱𝗲𝘀𝗰𝗿𝗶𝗯𝗲: to be complete, the documentation for a variable or method must be extended.

𝗡𝗼𝗻𝗼𝗯𝘃𝗶𝗼𝘂𝘀 𝗰𝗼𝗱𝗲: the behavior or meaning of a piece of code cannot be understood

## From youtube talk

https://www.youtube.com/watch?v=bmSAYlu0NcY

course : https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lectures.php

https://lethain.com/notes-philosophy-software-design/

- Most important concept in this field is decomposition of a problem and build it relatively easily.
- Idea of software design is doing things today to make it easier to develop in the future
-  One thing that determines high and low performers is practise
- Iterative process of building a system, use code reviews to edit and improve, then build from scratch
- General list
  - Working code is not enough, must minimise complexity
  - complexity comes from dependencies and obscruity
  - strategic vs tactical Programming
  - Classes should be deep
  - General purpose classes are deeper
  - new layer new abstraction
  - Comments should describe things that are not obvious from the code
  - Define errors out of existance
  - pull complexity downwards
- Class should not have large interface or lots of dependencies or side effects (this is the complexity) and not much funcitionality (impementation)
- Class should have small interface and deep functionality.
  - Apply to methods/classes/modules
- Shallow classes are an example of just calling another dependency's method
  - Issue with advice that classes/methods should be small, this  leads to shallow classes
  - EG filestream, buffered stream in java library. Need to create lots of objects instead of using one object
  - IT is not about length of class, it is about lots of abstractions
- Example of deep interface, Unix file i/o, wiht five methods
  - Lots of implementation details hidden

- Define errors out of existence
  - https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=exceptions
  - Huge source of complexity
  - Common wisdom: detect and throw as many exceptions
  - OVerall goal: minimise number of places where exceptions must be handled
  - Aim redefine the exception, so it does not exist, make normal behavour do the right things
    - ie java substring, throws lots of exceptions, instead better to return empty string if some error, if indexs are wrong sort it out (use correctly)
  - program defensively, but dont let exceptions be thrown
  - WHat matters in throwing an exception
  - Best to throw exceptions isntead of error code if it is propagate up, if caught immediately then use error code.
  - Crashing best for out of memory exceptions, to hard to catch
- Tactical vs strategic (mindset)
  - wrong approach is tactical
    - results in bad design, high complexity
    - quick fixes, shortcuts
    - short termism, get it working
    - problems start off small, and become speghetti exponentially
  - Workign code is not enough
  - Strategic
    - goal: produce great design
    - simplify future dev
    - minimise complexity
    - must sweat the small stuff
    - Take extra time today, will pay off in future
  - Complexity is inevitable, can slow it down
  - Most startups are tactical
    - get product out as fast as possible
    - hard to repair
    - Facebook
      - move fast break things
      - unstable hard to use codebase
      - mantra change to move fast with solid infrastructure
  - Get product out fast is to get best programmers, programmers want to work with clean code bases
  - How much to invest
    - 10 -20 %
    - Make small changes
      - For new codebase
        - careful design
        - good documentation
      - existing codebase
        - look for improvements
        - dont settle for few modified lines of code
        - Goal: After change, system should be the way it would have been if designed from the start
  - Layers are good for handling abstraction
    - problem is having too many skinny layers

Quotes

- Complexity is anything that makes software hard to understand or to modify.
- Isolating complexity in places that are rarely interacted with is roughly equivalent to eliminating complexity.
- Complexity is more apparent to readers than to writers. If other people think a piece of code is complex, it is.
- Change amplification is when making a local change requires many changes elsewhere, and is best prevented when you reduce the amount of code that is affected by each design decision, so design changes don't require very many code modifications.
- Complexity is caused by obscurity and dependencies.
- Dependency is when code can't be understood in isolation.
- Obscurity is when important information is not obvious.
- This can often be due to lack of documentation.
- Complexity is incremental, the result of thousands of choices. Which makes it hard to prevent and even harder to fix
- Tactical mindset is focused on getting something working, but makes it nearly impossible to produce good system design.
- Strategic programming is realizing that working code isn't enough. The primary goal is a good design that also solves your problem, not working code.
- you should be doing lots of incremental design improvement work over time.
- different than just "doing Agile", because Agile is too focused with features, whereas
  - The increments of development should be abstractions, not features.
  - Ideally, when you have finished with each change, the system will have the structure it would have had if you had designed it from the start with that change in mind.
- payoff for good design comes quickly. It's unlikely that tactical approach is faster even for the first version, let alone the second.
  - arguemnet against yagni
- The most important way to manage complexity is by shifting it from interfaces and into implementation:
  - Modules are interface and implementation.The best modules are where interface is much simpler than implementation.
  - It's more important for a module to have a simple interface than a simple implementation.
- An abstraction is a simplified view of an entity that omits unimportant details. Omitting details that are important leads to obscurity, creating a false abstraction.
- Each module should encapsulate a few pieces of knowledge, which represent design decisions. This knowledge should not appear in its interfaces,and hence are restricted to its implementation.Simpler interfaces correlate with better information hiding.
- The opposite of information hiding is information leakage:
  - When a design decision is used across multiple modules, coupling them together.
- Design it twice, taking radically different approaches.
- If you're not making the design better, you are probably making it worse.


## Nature of complexity

- Aim of software design is to minimise Complexity
- The skill of recognising complexity is essential
  - Choose good from a range of options
  - identify problems before investing a lot of time iin them
- Complexity is anything related to a system that makes it hard to understand or modify
- Complexity is found from the reader than the writer.
- Symptons of Complexity
  - Change amplification
    - Simple change in system, requires many modifications in many places
    - Goals is to reduce the amount of code that is affected by each design decision
  - Cognitive Load
    - How much a dev need to konw in order to complete a task
    - high load, more learning, more risk of bugs
    - Examples : apis with many methods, global variables, inconsistencies, dependencies between Modules
    - Number lines does not equaly complexity
  - Unknown unknowns
    - which part of the system to makes the changes to, or what info does the dev need to complete the task
    - consequence occurs when bugs are raised
- Aim: A make the system obvious
- What causes complexity: Dependencies and obscruity
  - dependency is when a given part of the system cannont be changed or understood isolation.
  - Goal: reduce dependencies, make them simple and obvvious
  - Obscruity occurs when important info is not obvvious
    - generic variable names
    - variables names wihtout units
    - Not obvious that dependencies exist
    - inconsistencies, ie same variable name used for two different purposes
    - Occurs from inadequate documentation
      - Clean design, less need for documentation
- Complexity is incremental
- In large systems and as they get bigger complexity increases naturally


## Working code is not enough

- Tactical mindset - promtoted by organisations
  - focus on getting as many features out as possible
- Strategic mindset - takes time, to get good design and fix problems
  - focus on long term
- Tactical programmning
  - get feature or bug fix, but hard to produce good design
  - short sighted
  - leads to complexity
- Stategic programming
  - understand working code is not enough
  - not acceptable to introduc Complexity
  - Most code in a system is written by extending the codebass, so need to be able to facilitate This
  - focus on different ways the system will change and how you will facilitate this
  - good documentation and tests
  - when design problem is found, fix it
- How much to invest
  - Waterfall (design upfront) is not effective
  - Better to make small investments on a continual basis
    - leads to longer time to complete
    - benefits will occur later on
  - Tactical programming, will be faster at first but slower later on
- Startups and investments
  - a lot of pressure on startups to get features out
  - They become tactical, and hope to hire more engineers as they get more successful
  - Once code turns to speghetti it becomes harder to work with
  - quality engineers leads to success
    - As they care about good design
  - Bad code base, hard to hire and retain engineers
  - Example facebook

## Modules should be deep

- Design systems so devs only need faces a small fraction of the overal complexity at any given time.
- Modular design
  - Defn: system is decomposed into a collection of modules that are relatively independent.
  - Examples of modules: classes, subsystems, services
  - Ideal: all modules completely independent, deve can work on one without knowledge of the others
  - The complexity of a system is that of the complexity of the worst module
  - Ideal impossible, as modules must be able to work together and call each others functions/methods
    - Thus must know about the other modules
    - thus dependencies will form
      - if one module changes, other modules dependent on it will need to change
      - ie arguments in a method chagne, then any other module usin this method will need to change too
  - Aim: minimise dependencies between modules
  - A module has a
    - Interface
      - has everything that you need to know about a module that you will use ie signatures of methods
      - What a module does
    - Implementation
      - The code that carries out the promise made by the interface
  - Methods withing a classs that is not oo is a module in itself
  - Higher levels subsystems or services, have interfaces of different forms
    - kernal calls or http requests
  - Best Modules: interfaces are simpler than implementation
    - simple interfaces -> minimises Complexity
    - If module changes without changes to interface, other modules will not be affected
- Whats an inteface
  - Contains formal
    - signature, names and types of params and return value, exception throw for the public methods
    - enforced by language
  - informal
    - high level behaviour, what it does ie naming
    - constraints on usage ie one method should be called before another
    - Derived by name or comments
- Abstractions
  - defn: a simplified view of an entity which omits unimportant details
    - helpl think and manipulate complex things
  - Each module provides abstraction by its interface
  - More unimportant details ommitted the Better
  - Can wrong
    - include details that are not unimportant -> abstractions become more complex
    - omits details that are important -> obscruity,not info to use it correctly
- Deep modules
  - Provide powerful functionality with simple interface
  - eg unix io and garbage collection
- Shallow modules
  - complex inteface simple implementation
  - ie java i/o need many classes, dependencies to work with filestream
- Interface should be designed to make common case as simple as possible
- Having lots of options (ie use of lots of classe, decorators) is useful too, a way to disable the default

## Information Hiding

- Create deep modules
- Info hiding
  - each module should encapsulate a few pieces of knowledge which represent design decision
  - Includes algorithm and data structures
  - Reduces complexity of interface
  - Makes it easier to evolve system
    - If algorithm changes, the interface does not need to only impl
  - Using private modifier is not info hiding but can help
    - But using getters/setters can still expose private members
- Information leakage
  - opposite of hidding
  - design design is represented in a lot of Modules
    - creates dependencies between those modules, and changes need to occur in them all
  - info leaked in interface
  - different classe know about file Information
  - Pull info out of affected class into new class, which has a simple interface
    - otherwise replace backdoor leakage with leakage through interface
- Temporal Decomposition
  - structure of system corresponds to the time order in which operations occur
  - Calling multiplemethods from different classses in specific order
    - better to put them in one class
  - In module design, focus on knowledge thats needed to perform task not theorder tasks Occurs
- Lots of classes can lead to info leakage
- Info hiding can be imporved by making class larger
  - All info that is needed to do the job of the interface is in here
  - Rather than have separate methods for each step (and thus have complex interface)
- Avoid exposing external data structures

## General purpose modules are deeper

- A module has two purposes
  - general - address a broad range of problems
    - Build for future
    - what about yagni?? features not used as hard to tell the future
    - Being too general purpose, might not actually solve the problem
  - special - only a few
    - YAGNI
    - what is needed
    - can always refactor later
    - For incremental development
- MAke classes somewhat special purpose
  - The module implementation should reflect your current needs, your interface should be general
  - general purpose approach allows for reuse and save time in future
  - general purpose better for simplicity even if it is used in one place
- Questions to ask
  - what is the simplest interface taht will cover my current needs?
    - can reduce number of methods without reducing overall functionality.
    - if have to introduce lots of params to reduce no. of methods not changing things
  - In how many situations will this method be used?
    - If several methods can be replaced with one
  - Is api easy to use for my current needs?
    - STop you from going to far
    - Having to write a lot more code to make it general is not a good thing


## Different layer, different abstraction

- systems are composed of layers
  - higher layers use lower layers functionalities
- Each layer provides different abstraction to the layers above and below
- Red flag: adjacent layers with similar abstraction. Decompositon problem
- Pass through methods
  - red flag
  - defn: has little implementation and invoke another method whose signature is similar/identical to that of the calling method
    - delegating all implementation to another method
  - not a clean division of responsibilities between classe
  - Make classes shallow (bad), increase interface complexity, not increase in functionality
  - Create dependecies between modules
  - The interface to a piece of functionality should in the same class that implements the functionality
  - There is an overlap of responsibilities between two classes
  - ACtion: Refactor so both clases has distinct responsibilities
    - expose lower level class directly to the callers of the high level class
    - Redistribute features between classes
    - merge classes if cannot be distangled
- When is interface duplication ok
  - Same signature methods  is alright if each method has significant different functionality.
  - Dispatcher (type of pass through but good)
    - uses arg/s to select on of which of several methods to invoke, then passes most/all of its args to choosen method, which implements specific algorithm
  - interfaces with multiple implementations
    - strategy pattern
- Decorators
  - Api duplication across layers
  - Defn: decorator object takes an existing obj and extends its funcitionality
    - it provides an api similar/identical to the underlying obj
    - its methods invoke the underlying object methods
    - decorator adds new methods when wrapping the underlying object
  - Why?
    - separate special purpose extensions of a class from a more generic core
  - Shallow , lots of boiler plate, lots of pass through methods
  - java i/o
  - Alternatives
    - add the functionality to the underlying class
      - if the functionality is general purpose or logically connected to class or it will be used often from this class
    - Merge into same class which it will be called if only used in this in class
    - Merge into exisiting decorator
    - Does it need to wrap exisiting functionality? Be a stand alone class to inject into another
- Interface versus implementation
  - The interface of class should be different to its implementation
    - internal should be different to external
    - What it does and how it does it should not be shown to be the Same
- Pass through variables
  - variables that passed down through long chain of methods
  - Add complexity as intermediate methods must be aware of its existence, even if they dont use it.
  - Make changes hard to do if that variable that is passed is now used differently
  - ACtion
    - see if there is shared object between the methods, and just pass that object
      - but again this will be passed through
    - store in global variable
      - issues: cannot store create two independent instances of the same system in the same process, globals will conflict ie in testing
    - use context object pattern.
      - stores all of the applications global state
      - one context object per instance of the system
      - Issue needed in many places and can end up being a pass through
      - a reference to the context can be saved in most of systems major objects
        - When it is needed, the object that needs it upon instantiation it passed it to its constructor
        - wiring
      - properties

## Pull complexity downwards

- In module have unavoidable complexity , options:
  - let users of module deal with it
  - If complexity is related to functionality of the module -> handle complexity internally within the module
- Most modules have more users than developers -> developers to suffer for user
- dev to make life easier for user of module
  - simple interface over simple implementation
- Dont give the hard problems to someone else
- If dont know how to handle it -> throw exception for caller to handle it
- have config/properties setting to decide what is best for them
- Amplifies problems
  - exception thrown ->every caller will deal with it
  - exports config, SAs will need to implement for each env
- Config params
  - moving complexity upwards instead of downwards
  - tuning the system for their system for requirements or workloads or env
  - The user might know better than the code what the best policy is
  - Can avoid dealing with issues and passing the on
    - imposssible to know these values
    - or can be determined automatically in codebase
  - config can end up out of date
  - Will a user be able to determine a better value than we can determine?
  - Can provide prop but with default in code
- TAking it too far
  - Too far, pulling all functionality down to one class
  - Only pull down functionality:
    - if it is closely related to the class's exisiting functionality
    - if it will result in many simplifications else in module/app
    - if it will simplify the interface

## Better together or better appart

- Fundamental Question:
  - given two pieces of functionality, should they be implemented together in the same place, or should tehir implementation be seperated?
- Applies at all levels of system: func, methods, classes and services
- Idea: split into small components, the smaller they are, the simpler they are
  - problem:
    - More components, harder to keep track of them. More interfaces, every new interface -> increase complexity
    - More code to manage.
    - Creates seperation. components will be further apart. Harder to see components and logic at same time, or aware of existence.
      - If truly independent then seperation is good.
      - If there is a dependency, then seperation is bad as fliping between components. Not aware of dependecies -> bugs
    - lead to duplication
- when to bring pieces together, if cloesly related:
  - they share information.
  - they are used together at the same time. Only if bi directional
    - ie disk block cache uses hash table, but hash table is not only used by it
  - OVerlap conceptually, there  is a higher level category that includes both components
  - Hard to understand if both are not together
- Info is shared
  - to do implementation of both. put together and reduces duplicaiton
- Simplify interface
  - Simplifies interface of module, when combing modules, if original modules only implement part of the solution
  - Can do things automatically, without user having to do it (ie call one method insted of several in certain order etc)
    - Can have flags to decide to turn off or switch out default behavour to custom behavour
- Elimntate duplication
  - extract method refactor
    - if replacement code is long, and method have simple signature
  - Snippet only has to be executed in one place.
    - ISsues with goto statement
    - call method, extract method
- Seperate general purpose and special case code
  - If module contains code used in several differen places, then it should support general purpose mechanism.
  - Special purpose code associated with general purpose mechanism should go in a different module, typically one associated with smae purpose.
  - In general, lower layers tend to be more general purpose and the upper layers more special purpose
    - Top most layers have featurs totally specific to the application
    - ie layered architecture, upper layers is core, lower layers is infrastructure and presentation. If used in both, ie usecase, then have interface for lower layers used instead of implementation in dependency.
- Splitting and joining methods
  - length of method is not a criteria for splitting
  - splitting creates more interfaces -> increase complexity
  - Only split if makes it simpler
  - if blocks of code have complex interaction, keep together
  - if simple to read then length is not a problem
  - having to flip between methods is Harder
  - Each method should do one thing and do it completely
  - Methods should have clean and simple interface, and should be deep
  - Refactor by extracting subtask
    - subtask should be independent of parent
    - parent should know nothing of how the child works
    - subtask should be general purpose
  - Refactor by splitting into two separate methods each visible to the calling method of the original
    - do when original has a complex interface or does too many thigns
    - should not need to call both split methods
  - Join methods if original methods are shallow or simpler interface
  - Red flag: Conjoined methods
    - cannot understand one method without understanding the other

## Define Errors out of existence

- exceptions can lead to complexity
- reduce number of places where exceptions must be handled
- End up not throughing exceptions by dealing with them
- Why exceptions add complexity
  - Def: Exception is any uncommon condition that alter the normal flow of control of a program
  - fault tolerant systems need to be able to deal with exceptions, without breaking the system
  - Ways of dealing wiht exceptions
    - Move forward and deal with work despite the exception
    - abort the process and report it upwards
  - exception handling code must restore consistency to the system ie rewinding any partial state changse
  - One exception can lead to another one, especially during recovery from first exception.
- Too many exceptions
  - Being too over defensive and defining too many exceptions is bad
  - Exceptions increase Complexity
  - People use exceptions to avoid dealing with difficult design decisions
    - thus it must be handled by the caller
  - Exception thrown by a class is part of the interface, thus increase complexity of interface
  - Reduce number of places where exceptions have to be handled
- Define errors out of existence
  - Define api so there are no exceptions to handle
  - Define the implementation to avoid throwing exception
- Example
  - When deleting do it async so that no need to check for other processes that are using it. Rather, mark it for deletion and no other process can use it and wait for the file to be finished if being used, then delete.
-
