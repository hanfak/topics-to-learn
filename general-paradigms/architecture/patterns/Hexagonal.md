# Hexagonal architecture

![](general-paradigms/architecture/diagram/hexagonal-architecture.png?raw=true)

- Within the hexagon, we find our domain entities and the use cases that work with them.
  - he hexagon has no outgoing dependencies, all dependencies point inwards
- Outside of the hexagon,
  - we find various adapters that interact with the application.
    - There might be a web adapter that interacts with a web browser, some adapters interacting with external systems and an adapter that interacts with a database.
  - The adapters on the left side are adapters that drive our application
    - because they call our application core
  - the adapters on the right side are driven by our application
    - because they are called by our application core
- To allow communication between the application core and the adapters, the application core provides specific ports.
  - For driving adapters,
    - such a port might be an interface that is implemented by one of the use case classes in the core and called by the adapter.
  - For a driven adapter,
    - it might be an interface that is implemented by the adapter and called by the core.
- The outermost layer consists of the adapters that translate between the application and other systems
  - Next, we can combine the ports and use case implementations to form the application layer, because they define the interface of our application.
  - The final layer contains the domain entities

## Why?

- we can decouple our domain logic from all those persistence and UI specific problems and reduce the number of reasons to change throughout the codebase.
  -  less reasons to change means better maintainability.
- The domain code is free to be modelled as best fits the business problems while the persistence and UI code are free to be modelled as best fits the persistence and UI problems.

## When to use?

- Ueful, if we’re building an application with rich business rules that can be expressed in a rich domain model that combines state with behavior
- If we’re building a CRUD application that simply stores and saves data, an architecture like this is probably overhead and no need
