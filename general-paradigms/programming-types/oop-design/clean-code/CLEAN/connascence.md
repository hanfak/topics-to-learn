# Connascence

## What

- Two components are connascent if a change in one would require the other to be modified in order to maintain the overall correctness of the system.
-  Connascence gives us an insight into the long-term impact our code will have on flexibility, as we write it. Maintaining a flexible codebase is essential for maintaining long-term development velocity.
- Connascence is a metric
- shared vocabulary for determining different types and the severity of the coupling in our systems

### Static

- source-code-level coupling
- which analyses calls at compile time.
- the degree to which something is coupled, either afferently or efferently

#### Connascence of Name (CoN)

- Multiple components must agree on the name of an entity
- Names of methods represents the most common way that code bases are coupled and the most desirable
- Tooling makes it easy to do system wide changes

#### Connascence of Type (CoT)

- Multiple components must agree on the type of an entity
- common facility in many statically typed languages to limit variables and parameters to specific types.
- Not just for static typed languages, as some languages offer selective typing

#### Connascence of Meaning (CoM) or Connascence of Convention (CoC)

- Multiple components must agree on the meaning of particular values.
- ie hard-coded numbers rather than constants and issues swapping them

#### Connascence of Position (CoP)

- Multiple entities must agree on the order of values.
-  issue with parameter values for method and function calls even in languages that feature static typing.

#### Connascence of Algorithm (CoA)

- Multiple components must agree on a particular algorithm.
- ie defines a security hashing algorithm that must run on both the server and client and produce identical results to authenticate the user. Obviously, this represents a high form of coupling—if either algorithm changes any details, the handshake will no longer work.

### Dynamic

- which analyses calls at runtime.
- No issues at compile time
- harder time determining dynamic connascence because we lack tools to analyze runtime calls

#### Connascence of Execution (CoE)

- The order of execution of multiple components is important.
- Wont work if for example using setter injection, but not everything is setup correctly before calling an instance method

#### Connascence of Timing (CoT)

- The timing of the execution of multiple components is important
- ie a race condition caused by two threads executing at the same time, affecting the outcome of the joint operation

#### Connascence of Values (CoV)

- when several values relate on one another and must change together
- ie changing one thing might affect the something else (dependency), so must change others together
- ie api contract can change that breaks consumers
- ie to maintain integrity of data structure, must change all, like changing a single point of corner of rectangle, must change others to maintain rectangle
- ie distributed transactions
  -  needs to update a single value across all of the databases, all the values must change together or not at all (rollback to previous state)

#### Connascence of Identity (CoI)

- when several values relate on one another and must change together.
-  involves two independent components that must share and update a common data structure, such as a distributed queue.

###  Properties

- Connascence is an analysis tool
-  where each instance of connascence in a codebase must be considered on three separate axes: strength, degree, locality
- consider strength and locality together
- Can use this formula
  - Connascence = Strength x Degree / Locality

#### strength

- Stronger connascences are harder to discover, or harder to refactor.
- the strength of connascence is determined by the ease with which a developer can refactor that type of coupling
- improve the coupling characteristics of their code base by refactoring toward better types of connascence
-  should prefer static connascence to dynamic because developers can determine it by simple source code analysis
-  the case of connascence of meaning, which developers can improve by refactoring to connascence of name
  -  in order to make informed decisions about when they will permit certain types of coupling, and when the code ought to be refactored.
- refactor up, from dynamic to static
  - identity -> value -> timing -> execution -> position -> algorithm -> meaning -> type -> name

#### Degree

-  An entity that is connascent with thousands of other entities is likely to be a larger issue than one that is connascent with only a few.
- Describes how many components are coupled.
  - the size of its impact— does it impact a few classes or many
-  Lesser degrees of connascence damage code bases less
- having high dynamic connascence isn’t terrible if you only have a few modules.
  - But codebases tend to grow

#### Locality

- Describes how close the coupled components are. A high locality is better and means coupled components are in the same module
-  Connascent elements that are close together in a codebase are better than ones that are far apart.
- measures how proximal the modules are to each other in the code base.
- Proximal code (in the same module)
  -  has more and higher forms of connascence than more separated code (in separate modules or code bases).
-  forms of connascence that indicate poor coupling when far apart are fine when closer together.
- ie
  -  two classes in the same component have connascence of meaning,
    - it is less damaging to the code base than if two components have the same form of connascence.

## How to use

- To improve modularity
  1. Minimize overall connascence by breaking the system into  encapsulated elements
  2. Minimize any remaining connascence that crosses encapsulation boundaries
  3. Maximize the connascence within encapsulation boundaries
- Rule of Degree:
  - convert strong forms of connascence into weaker forms of connascence
- Rule of Locality:
  - as the distance between software elements increases, use weaker forms of connascence
- Minimize overall connascence by breaking the system into encapsulated elements.
- Minimize any remaining connascence that crosses encapsulation boundaries.
- Maximize the connascence within encapsulation boundaries.
## connascence and Coupling


## Links

- https://connascence.io/
- https://thoughtbot.com/blog/connascence-as-a-vocabulary-to-discuss-coupling
- https://codesai.com/posts/2017/01/about-connascence
