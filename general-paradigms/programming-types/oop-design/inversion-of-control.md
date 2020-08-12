# Inversion of control

Related to DIP

- Inversion of Control is a concept that states that objects should not create their own dependencies, but rather the control of dependency creation should be inverted and given to something else

- a method of removing responsibilities from a class to make it simpler and less coupled to the rest of the system. inversion of control is not having to know who will create and use your objects, how, or when. It is about being as dumb and oblivious as possible, as having to know less is a good thing for software design.

- Dependency Injection and Service Locator design pattern is specific implementation that falls under the more generic umbrella term of IoC

- a practical implementation of IoC through the use of a Dependency Injection Container (DIC) such as Guice, Spring

- IOC is also referred to as “the Hollywood principle” because the subject of IOC is being told, “Don’t call us, we will call you.”
  - this means your classes do not have to know when their instances are created, who is using them, or howtheir dependencies are put together.
  - Your classes are plugins, and some external force will decide how and when they should be used

 ## Dependency Injection Containers

- Instead of you being in control of creating instances of your objects and invoking methods, you become the creator of plugins or extensions to the framework
  - The IOC framework will look at the web request and figure out which classes should be instantiated and which components should be delegated to

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
  - Stubbing out dependencies for testing becomes easier
  - Reduce amount of code and complexity
  - You can create plugins for your framework
  - Each plugin is independent and can be added or removed at any point in time.
  - Your framework can auto-detect these plugins, or there is a way of configuring which plugin should be used and how
  - Your framework defines the interface for each plugin type and it is not coupled to plugins themselves

- Negatives
  - stuck in the way of doing it, must follow convention of framework
  - New learning if not popular framework
  - Doing something outside of what the framework want can be very hard
  - Lots of magic, reflection, cached proxy
  - Another thing to upgrade, which if framework not used properly can affect the whole code base

- Can also do this, by newing up objects in another class (wiring//config) where the dependencies are inverted

## Links

- https://www.yegor256.com/2017/05/10/inversion-of-control.html

- https://completedeveloperpodcast.com/episode-165/
