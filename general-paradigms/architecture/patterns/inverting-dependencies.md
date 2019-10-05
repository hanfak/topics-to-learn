# Inverting dependencies

This is the key to good architecture, and the essance of what clean architecture is built on.

Inverting dependencies allows our architecture to maint SRP and DIP of SOLID.

## The Single Responsibility Principle

- A component should have only one reason to change.
- we don’t have to worry about this component at all if we change the software for any other reason, because we know that it will still work as expected.
- it’s very easy for a reason to change to propagate through code via the dependencies of a component to other components
- if component has a dependency, then if that dependency changes, the component might have to change
- we notice that the upper layers have more reasons to change than the lower layers.

## The Dependency Inversion Principle

- We can turn around (invert) the direction of any dependency within our codebase
-  layered architecture, the cross-layer dependencies always point downward to the next layer.
- due to the domain layer’s dependency to the persistence layer, each change in the persistence layer potentially requires a change in the domain layer
- But the domain code is the most important code in our application! We don’t want to have to change it when something changes in the persistence code!
- Thus domain is not beholden to changes in persistence when DIP is used

example 1 = Coupled, poor

----- Domain -------------------
|                               |
|     |-------service -----|    |
|     |                    |    |
------|--------------------|-----
      |                    |
      |                    |
------|-- Persistence -----|------
|     \/                    \/    |
|   Entity <---------- Repository |
|                                 |
-----------------------------------

Example 2: Applying dependency inversion

----- Domain -------------------
|                               |
|     |-------service -----|    |
|     \/                   \/   |
|    Entity          Repository |
|                    interface  |
|                          /\   |
---------------------------|-----

--------- Persistence -----|------
|                          |      |
|   Entity <---------- Repository |
|   for            implementation |
|   repository                    |
-----------------------------------
