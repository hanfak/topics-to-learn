# Inversion of control

Related to DIP

Inversion of Control is a concept that states that objects should not create their own dependencies, but rather the control of dependency creation should be inverted and given to something else

Dependency Injection and Service Locator design pattern is specific implementation that falls under the more generic umbrella term of IoC

 a practical implementation of IoC through the use of a Dependency Injection Container (DIC) such as Guice, Spring

 ## Dependency Injection Containers

- DIC provides:
  - Creates objects that other objects need (i.e. their dependencies)
    - When DIP is applied, a graph of objects, each with their own dependencies, can have those dependencies supplied to them
      - via constructor params
  - Controls the lifetime of the objects that it creates
    - supplying the same object instance (singleton) for all dependencies of a given kind.
  - Creates objects for dependencies all the way down an object hierarchy

- Pro of DIC
  - is that wiring of objects dont need to be changed
  - Using an auto-wired DIC means that the architecture (dependencies) of the system are not hard- coded
  - Dependencies can be added and removed (for example constructor parameters) and classes can be refactored and combined without having to spend time coding how those dependencies are provided.

- Can also do this, by newing up objects in another class (wiring//config) where the dependencies are inverted
