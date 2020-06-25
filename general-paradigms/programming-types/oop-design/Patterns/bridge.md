# Bridge Pattern

## What

- A pattern to decouple an abstraction from its implementation so that the two can vary independently.
- Bridge patterns decouple the abstract class and its implementation classes by providing a bridge structure between them.

## Why

- When we want a parent abstract class to define the set of basic rules, and the concrete classes to add additional rules
- When we have an abstract class that has a reference to the objects, and it has abstract methods that will be defined in each of the concrete classes
- The bridge pattern is useful when both the class and what it does vary, often because changes in the class can be made easily with minimal prior knowledge about the program.
- The bridge pattern allows us to avoid compile-time binding between an abstraction and its implementation. This is so that an implementation can be selected at run-time.
  - Selection or switching of implementation is at run-time rather than design time.
- You want to hide implementation details (changes) from clients.
- Abstraction and implementation should both be extensible by subclassing.
- You want to share an implementation among multiple objects and this should be hidden from the client.
- Reduction in the number of sub classes – Sometimes, using pure inheritance will increase the number of sub-classes.
- Improved Extensibility – Abstraction and implementation can be extended independently.
- Loosely coupled client code – Abstraction separates the client code from the implementation. So, the implementation can be changed without affecting the client code and the client code need not be compiled when the implementation changes.

## How

-The abstraction is an interface or abstract class, and the implementer is likewise an interface or abstract class. The abstraction contains a reference to the implementer. Children of the abstraction are referred to as refined abstractions, and children of the implementer are concrete implementers. Since we can change the reference to the implementer in the abstraction, we are able to change the abstraction’s implementor at run-time. Changes to the implementer do not affect client code.

## Drawbacks

- Increases complexity.
- Double indirection – This will have a slight impact on performance. The abstraction needs to pass messages along to the implementator for the operation to get executed.
-  You might make the code more complicated by applying the pattern to a highly cohesive class.

## When

- Use the Bridge pattern when you want to divide and organize a monolithic class that has several variants of some functionality (for example, if the class can work with various database servers).
- Use the pattern when you need to extend a class in several orthogonal (independent) dimensions.
-  Use the Bridge if you need to be able to switch implementations at runtime.

## Comparisons with other patterns

- Bridge makes them work before they are.
  - Adapter makes things work after they’re designed;
- Bridge is designed up-front to let the abstraction and the implementation vary independently.
  - Adapter is retrofitted to make unrelated classes work together.
- State, Strategy, Bridge (and to some degree Adapter) have similar solution structures.
  - They all share elements of the “handle/body” idiom. They differ in intent – that is, they solve different problems.
- The structure of State and Bridge are identical (except that Bridge admits hierarchies of envelope classes, whereas State allows only one).
  - The two patterns use the same structure to solve different problems:
    - State allows an object’s behavior to change along with its state,
    - while Bridge’s intent is to decouple an abstraction from its implementation so that the two can vary independently.
- If interface classes delegate the creation of their implementation classes (instead of creating/coupling themselves directly), then the design usually uses the Abstract Factory pattern to create the implementation objects.
- You can combine Builder with Bridge: the director class plays the role of the abstraction, while different builders act as implementations.
- You can use Abstract Factory along with Bridge.
  - This pairing is useful when some abstractions defined by Bridge can only work with specific implementations. In this case, Abstract Factory can encapsulate these relations and hide the complexity from the client code.
- Bridge, State, Strategy (and to some degree Adapter) have very similar structures. Indeed, all of these patterns are based on composition, which is delegating work to other objects. However, they all solve different problems. A pattern isn’t just a recipe for structuring your code in a specific way. It can also communicate to other developers the problem the pattern solves.

## Links

- https://dzone.com/articles/bridge-design-pattern-in-java
