# Adapter

## What?

- An Adapter pattern acts as a connector between two incompatible interfaces that otherwise cannot be connected directly.
- An Adapter wraps an existing class with a new interface so that it becomes compatible with the client’s interface.
- is to convert an existing interface into another interface that the client expects.
- adapters are used when we have a class (Client) expecting some type of object and we have an object (Adaptee) offering the same features but exposing a different interface.
- Similar to bride pattern but different
  - Adapter makes things work after they're designed; Bridge makes them work before they are.
  - Adapter is retrofitted to make unrelated classes work together. Bridge is designed up-front to let the abstraction and the implementation vary independently.
  - Adapter provides a different interface to its subject. Proxy provides the same interface. Decorator provides an enhanced interface.
  - Adapter is meant to change the interface of an existing object. Decorator enhances another object without changing its interface. Decorator is thus more transparent to the application than an adapter is. As a consequence, Decorator supports recursive composition, which isn't possible with pure Adapters.
  - Facade defines a new interface, whereas Adapter reuses an old interface. Remember that Adapter makes two existing interfaces work together as opposed to defining an entirely new one.

## When to use??

- When an outside component provides captivating functionality that we'd like to reuse, but it's incompatible with our current application. A suitable Adapter can be developed to make them compatible with each other
- When our application is not compatible with the interface that our client is expecting
- When we want to reuse legacy code in our application without making any modification in the original code
- The Adapter pattern is useful when you are trying to integrate components of your system that have incompatible interfaces. They perform a conversion of a target interface (the interface a client expects) to the adaptee’s interface.



## Why?

- Helps achieve reusability and flexibility.
- Impedance match an old component to a new system
- Client class is not complicated by having to use a different interface and can use polymorphism to swap between different implementations of adapters.
- Use for polymorphism, ie wrapping all adaptees in an adapter that has same inteface, then when iterating through this list of adapters, can use the same method instead ofdoing lots of if/else statements to find the instance of and casting.

## Drawbacks

- All requests are forwarded, so there is a slight increase in the overhead.
- Sometimes many adaptations are required along an adapter chain to reach the type which is required.

## Implementation

1. The client makes a request to the adapter by calling a method on it using the target interface.
2. The adapter translates that request on the adaptee using the adaptee interface.
3. Client receive the results of the call and is unaware of adapter’s presence.

## Facade vs Adapter

- both similar
- https://bambielli.com/posts/2017-09-09-the-adapter-pattern/
- https://gist.github.com/Integralist/d67f0f913d795f703b89
- https://stackoverflow.com/questions/2961307/what-is-the-difference-between-the-facade-and-adapter-pattern/2961400

## Links

- https://codurance.com/2015/04/15/design-patterns-in-the-21st-century-part-three/
- https://stackify.com/design-patterns-explained-adapter-pattern-with-code-examples/
