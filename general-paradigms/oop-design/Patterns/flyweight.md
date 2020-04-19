# Flyweight pattern

## What

- is used to reduce the memory footprint.
- allows programs to support vast quantities of objects by keeping their memory consumption low.
  - Pattern achieves it by sharing parts of object state between multiple objects. The Flyweight saves RAM by caching the same data used by different objects.
- It can also improve performance in applications where object instantiation is expensive.
- the flyweight pattern is based on a factory which recycles created objects by storing them after creation
  - Each time an object is requested, the factory looks up the object in order to check if it's already been created. If it has, the existing object is returned – otherwise, a new one is created, stored and then returned.
- The flyweight object's state is made up of an invariant component shared with other similar objects (intrinsic) and a variant component which can be manipulated by the client code (extrinsic).
- flyweight objects are immutable: any operation on the state must be performed by the factory.
- Elements
  - an interface which defines the operations that the client code can perform on the flyweight object
  - one or more concrete implementations of our interface
  - a factory to handle objects instantiation and caching

## Structure

- The Flyweight pattern is merely an optimization. Before applying it, make sure your program does have the RAM consumption problem related to having a massive number of similar objects in memory at the same time. Make sure that this problem can’t be solved in any other meaningful way.
- The Flyweight class contains the portion of the original object’s state that can be shared between multiple objects. The same flyweight object can be used in many different contexts. The state stored inside a flyweight is called “intrinsic.” The state passed to the flyweight’s methods is called “extrinsic.”
- The Context class contains the extrinsic state, unique across all original objects. When a context is paired with one of the flyweight objects, it represents the full state of the original object.
- Usually, the behavior of the original object remains in the flyweight class. In this case, whoever calls a flyweight’s method must also pass appropriate bits of the extrinsic state into the method’s parameters. On the other hand, the behavior can be moved to the context class, which would use the linked flyweight merely as a data object.
- The Client calculates or stores the extrinsic state of flyweights. From the client’s perspective, a flyweight is a template object which can be configured at runtime by passing some contextual data into parameters of its methods.
- The Flyweight Factory manages a pool of existing flyweights. With the factory, clients don’t create flyweights directly. Instead, they call the factory, passing it bits of the intrinsic state of the desired flyweight. The factory looks over previously created flyweights and either returns an existing one that matches search criteria or creates a new one if nothing is found.

## uses

- Data Compression
  - lossless compression algorithms
    - each flyweight object acts as a pointer with its extrinsic state being the context-dependent information.
  - usage is in a word processor.
    - Here, each character is a flyweight object which shares the data needed for the rendering. As a result, only the position of the character inside the document takes up additional memory.
- Data Caching
- storage costs are high because of the sheer quantity of objects
- most object state can be made extrinsic
- many groups of objects may be replaced by relatively few shared objects once extrinsic state is removed
- the application doesn't depend on object identity. Since flyweight objects may be shared, identity tests will return true for conceptually distinct objects.

## Intrinsic and Extrinsic States

- Suppose in a text editor when we enter a character, an object of Character class is created, the attributes of the Character class are {name, font, size}. We do not need to create an object every time client enters a character since letter ‘B’ is no different from another ‘B’ . If client again types a ‘B’ we simply return the object which we have already created before. Now all these are intrinsic states (name, font, size), since they can be shared among the different objects as they are similar to each other.
- Now we add to more attributes to the Character class, they are row and column. They specify the position of a character in the document. Now these attributes will not be similar even for same characters, since no two characters will have the same position in a document, these states are termed as extrinsic states, and they can’t be shared among objects.

## Advantages

- You can save lots of RAM, assuming your program has tons of similar objects.


## Drawbacks

- You might be trading RAM over CPU cycles when some of the context data needs to be recalculated each time somebody calls a flyweight method.
-  The code becomes much more complicated. New team members will always be wondering why the state of an entity was separated in such a way.

## Comparisons to other patterns

- You can implement shared leaf nodes of the Composite tree as Flyweights to save some RAM.
- Flyweight shows how to make lots of little objects, whereas Facade shows how to make a single object that represents an entire subsystem.
- Flyweight would resemble Singleton if you somehow managed to reduce all shared states of the objects to just one flyweight object.differences between these patterns:
  - There should be only one Singleton instance, whereas a Flyweight class can have multiple instances with different intrinsic states.
  - The Singleton object can be mutable. Flyweight objects are immutable.

## Links

- https://sourcemaking.com/design_patterns/flyweight/java/4
