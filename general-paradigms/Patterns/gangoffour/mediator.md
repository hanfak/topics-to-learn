# Mediator Pattern

## What

- Allows loose coupling by encapsulating the way disparate sets of objects interact and communicate with each other.  Allows for the actions of each object set to vary independently of one another.
- Reduce chaotic dependencies between objects ie cyclic dependencies

## How

- The Mediator defines the interface for communication between Colleague objects. The ConcreteMediator implements the Mediator interface and coordinates communication between Colleague objects. It is aware of all the Colleagues and their purpose with regards to inter communication.The ConcreteColleague communicates with other colleagues through the mediator.

## why

- Without this pattern, all of the Colleagues would know about each other, leading to high coupling.
  - By having all colleagues communicate through one central point we have a decoupled system while maintaining control on the object's interactions.
- in case we need to change the way Colleague objects work together, we only have to amend the ConcreteMediator logic
- helps in reducing the direct references to each other.
- Mediator helps in replacing “many-to-many” relationship with “one-to-many” relationships, so it is much easier to read and understand. Also the maintenance becomes easy due to centralized control of communication.
- It limits subclassing. A mediator localizes behavior that otherwise would be distributed among several objects.

## Drawbacks

- the Mediator object itself can become very complicated itself
  - The Observer pattern could help here, with the colleague objects dealing with the events from the mediator, rather than having the mediator look after all orchestration.
- It centralizes control. The mediator pattern trades complexity of interaction for complexity in the mediator. Because a mediator encapsulates protocols, it can become more complex than any individual colleague. This can make the mediator itself a monolith that’s hard to maintain

## When to use

- when the communication between objects is complicated, but well defined.
  - When there are too many relationships between the objects in your code
- The Mediator Pattern is a good choice if we have to deal with a set of objects that are tightly coupled and hard to maintain
- by using the mediator object, we extract the communication logic to the single component,
- we can introduce new mediators with no need to change the remaining parts of the system.

## Other

- Mediator pattern can be seen as a multiplexed facade pattern. In mediator, instead of working with an interface of a single object, you are making a multiplexed interface among multiple objects to provide smooth transitions.
