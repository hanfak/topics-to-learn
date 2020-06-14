# State Pattern

## What

- allow the object for changing its behavior without changing its class
- state-related behaviors into separate state classes and forces the original object to delegate the work to an instance of these classes, instead of acting on its own.
-  State pattern can be recognized by methods that change their behavior depending on the objects’ state, controlled externally.
- The State pattern is closely related to the concept of a Finite-State Machine.
  - The main idea is that, at any given moment, there’s a finite number of states which a program can be in. Within any unique state, the program behaves differently, and the program can be switched from one state to another instantaneously.
  - However, depending on a current state, the program may or may not switch to certain other states. These switching rules, called transitions, are also finite and predetermined.

## How

- The State pattern suggests that you create new classes for all possible states of an object and extract all state-specific behaviors into these classes.
- Instead of implementing all behaviors on its own, the original object, called context, stores a reference to one of the state objects that represents its current state, and delegates all the state-related work to that object.
- To transition the context into another state, replace the active state object with another object that represents that new state.
  - This is possible only if all state classes follow the same interface and the context itself works with these objects through that interface
- Structure
  - Context stores a reference to one of the concrete state objects and delegates to it all state-specific work. The context communicates with the state object via the state interface. The context exposes a setter for passing it a new state object.
  - The State interface declares the state-specific methods. These methods should make sense for all concrete states because you don’t want some of your states to have useless methods that will never be called.
  - Concrete States provide their own implementations for the state-specific methods. To avoid duplication of similar code across multiple states, you may provide intermediate abstract classes that encapsulate some common behavior.
    - State objects may store a backreference to the context object. Through this reference, the state can fetch any required info from the context object, as well as initiate state transitions.
  - Both context and concrete states can set the next state of the context and perform the actual state transition by replacing the state object linked to the context.
- How
  - Define a "context" class to present a single interface to the outside world.
  - Define a State abstract base class.
  - Represent the different "states" of the state machine as derived classes of the State base class.
  - Define state-specific behavior in the appropriate State derived classes.
  - Maintain a pointer to the current "state" in the "context" class.
  - To change the state of the state machine, change the current "state" pointer.
- Where the state transitions will be defined.
  - The choices are two:
    - the "context" object
      -  advantage is ease of adding new State derived classes
      - The disadvantage is each State derived class has knowledge of (coupling to) its siblings, which introduces dependencies between subclasses.
    - each individual State derived class.



## When

- The State pattern is commonly used in Java to convert massive switch-base state machines into the objects.
- when we are dealing with an object which can be in different states during it’s life-cycle and how it processes incoming requests (or make state transitions) based on it’s present state – we can use the state pattern.
-  Use the State pattern when you have an object that behaves differently depending on its current state, the number of states is enormous, and the state-specific code changes frequently.
  - you extract all state-specific code into a set of distinct classes. As a result, you can add new states or change existing ones independently of each other, reducing the maintenance cost.
- Use the pattern when you have a class polluted with massive conditionals that alter how the class behaves according to the current values of the class’s fields.
  - The State pattern lets you extract branches of these conditionals into methods of corresponding state classes. While doing so, you can also clean temporary fields and helper methods involved in state-specific code out of your main class.
- Use State when you have a lot of duplicate code across similar states and transitions of a condition-based state machine
  - The State pattern lets you compose hierarchies of state classes and reduce duplication by extracting common code into abstract base classes.

## Advantages

- reduce if/else statements.
- all logic for each of the states would not be spread out
- Introduce new states without changing existing state classes or the context.

## Drawbacks

- State pattern drawback is the payoff when implementing transition between the states. That makes the state hardcoded, which is a bad practice in general.


## Comparison with other patterns

- With strategy
  -  the strategy pattern defines a family of interchangeable algorithms. Generally, they achieve the same goal, but with a different implementation
    - In state pattern, the behavior might change completely, based on actual state.
  - in strategy, the client has to be aware of the possible strategies to use and change them explicitly.
    - in state pattern, each state is linked to another and create the flow as in Finite State Machine.
  - With Strategy, the choice of algorithm is fairly stable. With State, a change in the state of the "context" object causes it to select from its "palette" of Strategy objects.
- Bridge, State, Strategy (and to some degree Adapter) have very similar structures.
  - Indeed, all of these patterns are based on composition, which is delegating work to other objects.
  - However, they all solve different problems. A pattern isn’t just a recipe for structuring your code in a specific way. It can also communicate to other developers the problem the pattern solves.
- The structure of State and Bridge are identical (except that Bridge admits hierarchies of envelope classes, whereas State allows only one).
  - The two patterns use the same structure to solve different problems:
    - State allows an object's behavior to change along with its state, while Bridge's intent is to decouple an abstraction from its implementation so that the two can vary independently.
- State objects are often Singletons.
- Flyweight explains when and how State objects can be shared.
- Interpreter can use State to define parsing contexts.

## Alternatives

- Workflows and events
  - Depending on the event we are on, the workflow will determine which is the next event
  - can be used with aggregates ie DDD
- http://angry-architect.blogspot.com/2006/08/problems-with-state-pattern.html
