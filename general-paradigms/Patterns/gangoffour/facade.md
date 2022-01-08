# Facade Pattern

## What?

- a facade encapsulates a complex subsystem behind a simple interface. It hides much of the complexity and makes the subsystem easy to use.
- Used for complex complex systems of clases, libraries or frameworks
- Recognised by the use of a simple interface, but under the hood (implementation) is complex
- The client only interacts with the Façade class without knowing about the subsystem classes.
- The subsystem that the facade abstracts over doesnot know anything (not dependent) about the facade

## Why?

- Layering: Facade pattern can be used in applications for creating a layer to abstract and unify the related interfaces in the application. Use of a facade will define an entry point to each subsystem level and thus make them communicate only through their facades; this can simplify the dependencies between them.

### Benefits

-  It decouples a client implementation from the complex subsystem.
  - we can make changes to the existing subsystem and don't affect a client.
- Façade makes the API and libraries easier to use which is good for maintenance and readability.
-  It can collate and abstract various poorly designed APIs with a single simplified API.
- It reduces dependencies of the external code on the inner working of the libraries and thus providing flexibility.
- increases loose coupling

### Drawbacks

- Lead to lots of levels of abstraction and indirection
- Can be overused for simple implementations
- the subsystem methods are connected to the Façade layer. If the structure of the subsystem changes then it will require subsequent change to the Façade layer and client methods.
