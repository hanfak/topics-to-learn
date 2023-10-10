# Coupling

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Coupling](#coupling)
	- [What](#what)
		- [Accidental coupling](#accidental-coupling)
		- [Intentional coupling](#intentional-coupling)
	- [Levels of Coupling](#levels-of-coupling)
	- [Coupling Metrics](#coupling-metrics)
		- [Class Level](#class-level)
		- [Module Level](#module-level)
	- [Decoupling](#decoupling)
	- [Benefits of reducing coupling](#benefits-of-reducing-coupling)
	- [Examples](#examples)
	- [Law of Demeter (LoD)](#law-of-demeter-lod)

<!-- /TOC -->


## What

- Coupling is a measure of how much two components know about and depend on one another
  - It is a measure of quality
- **Aim to reduce coupling between objects**.
  - Trade off with other needs with the system
- Cannot have no coupling.
  - no coupling between components means that they are completely unaware of each other’s existence
-  the level of knowledge that one piece of code has about another piece of code that it is interacting with
  -  Having modules A and B, the more knowledge about B is required in order to understand A, the more closely connected is A to B. The fact that one module needs to be inspected in order to understand the operation of another is an indication of a degree of interconnection, even if the degree of interconnection is not known.
-  Coupling is affected by
  -  the type of connections between modules
  -  interface complexity
  -  information flow between module connections
  -  binding time of module connections
- Tight coupling means that one piece of code relies on the internal implementation details of code it collaborates with;
  - it uses knowledge of how the other code does something rather than just relying on it to do something.
- Loose coupling means that one piece of code does not rely upon, or even have knowledge of, the implementation details of the code it interacts with.
- keeping the relationship between objects intentional and clear
- code that is loosely coupled indirectly depends on the code it uses
- Can be achieved through use of an indirect call
  - Instead of calling a service directly (the concrete implementation of a class) it is called via an intermediary
  - Replacing the service will only affect the intermediary, reducing the impact of the change on the rest of the system.
- Should think in terms of **intentional** and **accidental** coupling
- Code has fewer side effects among entities, easier to test, reuse and extend
- If I have lots of unrelated dependencies, it is a coupling issue

### Afferent and efferent coupling

- Afferent coupling measures the number of incoming connections to a code artifact (component, class, function, and so on).
- Efferent coupling measures the outgoing connections to other code artifacts.

### Accidental coupling

- shows up when other code qualities are lacking
- EG If i have an uncohesive method that deals with many issues (has many responsibilities), I will have many unrelated reasons to couple with it.
- Avoid writing 'UBER apis'
  - they are fragile apis as they
    - try to do too much,
    - difficult to maintain and
    - couple code accross classes with that have no links to each other
  - IF different callers of an API share some of the same implementation or state for different reason, dont expose
  - ISP
    - create multiple apis that internally use only the part thats needed for each caller
- **Code reuse is good because it helps eliminate redundancy but at the expense of other code qualities**
-


### Intentional coupling

- TBC

## Levels of Coupling

- Can be either low / loose / weak or high / tight / strong
- Tight coupling translates into ripple effects when making changes, as well as code that is difficult to understand.
  - It tends to propagate errors across modules, when one module behaves incorrectly.
  - It tends to complicate debugging and fixing defects.
- Levels (From high to low)
  - **Content Coupling**:
    - Content coupling, or pathological coupling, occurs when one module modifies or relies on the internal workings of another module.
    - Changing the inner working will lead to the need of changing the dependent module.
    - An example would be a search method that adds an object which is not found to the internal structure of the data structure used to hold information.
  - **Common Coupling**:
    - Global coupling, or common coupling, occurs when two or more functions share global data.
    - Any changes to them have a ripple effect.
    - An example of global coupling would be global information status regarding an operation, with the multiple modules reading and writing to that location.
  - **External Coupling**:
    - External coupling occurs when one or more modules share a format, interface or communication protocol, that is imposed upon them.
    - This usually happens when modules are in direct communication with infrastructure layers, e.g., OS functions.
  - **Control Coupling**:
    - Control coupling occurs when one module controls the flow of another by passing control information,
    - e.g., a control flag, a comparison function passed to a sort algorithm.
  - **Stamp Coupling**:
    - Stamp coupling, or data structure coupling, occurs when modules share a composite data structure and use only a part of it, possibly different parts.
    - One example is of a print module that accepts an Entity, and retrieves its information to construct a message.
  - **Data Coupling**:
    - Data coupling occurs when methods share data, regularly through parameters.
    - Data coupling is better than stamp coupling, because the module takes exactly what it needs, without the need of it knowing the structure of a particular data structure.
  - **Message Coupling**:
    - Message coupling is the lowest form of coupling, realized with decentralization and message passing.
    - Examples include Dependency Injection and Observables.

## Coupling Metrics

- it can be quite subjective and requires personal judgement
- These are useful, but should not be solely relied upon define the best practises or implementation

### Class Level

- Class level coupling results from implementation dependencies in a system. In general, the more assumptions are made by one class about another, the tighter the coupling.
- The strength of coupling is given by the stability of a class,
    - i.e., the amount of changes in dependant classes that need be made if a class changes,
  - and the scope of access,
    - i.e., the scope in which a class is accessed, with the higher scope introducing tighter coupling.
- At class level, the degree of coupling is measured as the ratio of number of messages passed to the number of messages received,
  - i.e., DC = MRC / MPC
    - MRC is the received message coupling (the number of messages received by a class from other classes)
    - MPC is the passed message coupling (the number of messages sent by a class to other classes).
- Class level is a particular case of the Module level metric.

### Module Level

- A more general metric, this metric tracks other modules, global data, and outside environment.
- The formula computes a module indicator mc, where
  - mc = k / M
    - as the value of mc increases, the overall coupling decreases
  - with k a proportionality constant and M a value calculated by the following formula
    - M = di + (a * ci) + d0 + (b * c0) + gd + c * gc) + w + r
      - a, b, and c are defined empirically
      - w = the number of modules called (fan out)
      - r = the number of modules calling the module under consideration (fan-in) are environmental coupling parameters
      - gd and gc, describing the number of global variables used as data and as control, are global coupling parameters
      - di, do, ci, and co, describing the number of data and control input and output parameters, are data and control flow parameters
- In order to have the coupling move upward as the degree of coupling increases, a revised coupling metric, C, might be defined as
  - C = 1 - mc

## Decoupling

- Decoupling is the systematic coupling reduction between modules with the explicit intent of making them more independent
- Decoupling on the levels of coupling
  - Content coupling can be eliminated by following encapsulation.
  - Common coupling can be resolved by introducing abstractions. Design patterns could prove useful towards achieving a good architecture.
  - External coupling can be resolved by eliminating the knowledge of formats from the domain, and operating on concepts.
  - Control coupling can be eliminated by using strategies or states.
  - Stamp coupling can be eliminated by passing actual data.
  - Data coupling can be eliminated by employing message passing.
  -


## Benefits of reducing coupling

- It make code simpler and more extensible. In the process, it provides insights on the details of the processing of a particular piece of data. It makes you learn a lot about the corresponding part of the program, both in terms of code and in terms of business features.
- changes in private, internal implementation details do not ripple throughout the rest of the system.
- Makes it easeir to isolate, verify, reuse and extend
- Lets you put *seams* in your code so you can inject dependencies instead of tightly coupling them
- This helps with make code more testable, by using the seam to replace the dependency with a stub/mock.
- In loosely coupled systems, individual modules can be studied and altered without the need of taking into account a lot of information from other modules.
- Errors can be pointed out much more easily. Debugging takes less time, while fixing defects is usually simpler. The chances of error propagation across modules tend to be reduced.

## Examples

- A function remains coupled with another object because it accesses its data (via getters and setters)


- https://codurance.com/software-creation/2016/07/25/thoughts-on-coupling-in-software-design/
- https://martinfowler.com/ieeeSoftware/coupling.pdf
- https://mattjhayes.com/2020/04/18/it-architecture-a-discussion-on-coupling/

## Law of Demeter (LoD)

- known as Principle of Least Knowledge
- The principle states that a unit should only have knowledge of and talk to closely-related units, assuming as little as possible about the structures and properties of anything it interacts with, including its own subcomponents.
  - For example, an object A could call functionality on object B, but should not reach through B to access an object C for its functionality.
  - Instead, object B should facilitate access through its own interface, propagating the request to its subcomponents.
  - Alternatively, A could have a direct reference to C.
- Formal defintion
  - a method M on an object O can invoke the methods of the following objects:
    - O
    - M’s parameters
    - Any objects created / instantiated within M
    - O’s direct subcomponents
    - A global variable, accessible by O, in the scope of M
- an object should not call a method on a returned object,
  - i.e., there should be at most one dot in code, e.g., a.Method(), and not a.B.Method().
- talk only to your friends, not to strangers.
  - it is ok to make reference to immediate collaborators (“friends”) from a piece of code, but not the collaborators (strangers) of those collaborators.
- Reduces coupling
- when dealing with views (xml/json) it can be acceptable to reach into strangers’ data in order to display it.
- is it data or behaviour that is being wrapped/”delegated”. If it is behaviour then it can often be a better candidate for applying LoD than data.

### Issues

- when blindly applied to core classes and data structures, it leads to convoluted, over-de-coupled code that obscures behavior.
- The name is too rigid, it is not a law, you code will not break if you follow it
- it can be seen here http://labs.cs.upt.ro/labs/acs/html/lectures/6/res/Lieberherr-LawOfDemeter.pdf
	- Looks more nuanced definition
- Another location https://www2.ccs.neu.edu/research/demeter/demeter-method/LawOfDemeter/general-formulation.html
	- Each unit should have only limited knowledge about other units: only units “closely” related to the current unit.
- Should this be applied to domain objects, basically data structures
- comply with demeter, leads to more methods, more tests, more code, more stuff to look after
	- This leads to increase number of ways of getting something, violation of DRY

- https://naildrivin5.com/blog/2020/01/22/law-of-demeter-creates-more-problems-than-it-solves.html

## Integration Strength Vlad Khononov

Four key types most to least coupling
- intrusive coupling
  - more implicit interfaces
- functional coupling
- model coupling
- contract coupling
  - explicit interfaces

- Define a way of measure coupling along 3 axes
- Areas:
  - Strength
    - such as the level of knowledge sharing, the extent of communication between components, and the frequency of changes that affect both components.
    - Four key types most to least coupling
      - intrusive coupling
        - more implicit interfaces
        - have a strong reliance on each other's internal details and implementation. Changes to one component require simultaneous changes to the other to maintain proper functionality
      - functional coupling
        -  components rely on each other's functionality or services to accomplish specific tasks. However, they do not necessarily depend on each other's internal details and do not have detailed knowledge of each other's implementation.
      - model coupling
        - components share a common understanding and usage of the business domain or underlying data model. They interact based on a shared comprehension of the data's structure and meaning.
        - Issues occurs when model is constantly changing, which can have a cascading affect
      - contract coupling
        - explicit interfaces
        - components interact through explicitly defined interfaces or contracts. They communicate based on well-defined APIs, specifying the methods and data structures for interactions.
    
    - Distance
      - the physical or logical separation between two components in a software system. It represents how far apart the connected components are, either in terms of their physical location within the codebase or their logical boundaries.
      - Components that are located close to each other in the codebase or are tightly integrated are considered to have a short distance, while components that are far apart or loosely connected have a long distance.
      - The idea of cohesion
      - Components that work together to accomplish a specific task or are part of the same business domain are logically close, while those handling different functionalities are logically distant.
      - Components that are physically or logically close may have higher coupling, as changes in one component could directly impact the other.
      - components with a greater distance may have lower coupling, making them more independent and easier to maintain.
      - The greater the distance, the more coordination it takes to make a change
    - Volatility

### Coupling pain metric 

- High Strength + High volatility = high maintenance effort
- High Strength + High Distance = high cost of evolving the system
- High volatility +  High Distance = High coordination effort
- pain = volatility x strenght x distance 
  - Aim is to reduce one aspect to as low as possible
  - To make one arg 0 (lowest coupling)

### Links 
- https://youtu.be/eQOM-UrNTS4 Balancing Coupling in Software Design - Vlad Khononov - NDC Oslo 2023

## Links 

- https://www.youtube.com/watch?v=nNFgOtN9Gts Balancing Coupling in Software Design (Vlad Khononov)

- https://www.martinfowler.com/ieeeSoftware/coupling.pdf
