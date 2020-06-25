# Prototype

## what

- used when we have an instance of the class (prototype) and we'd like to create new objects by just copying the prototype.
- Example
  - In some games, we want trees or buildings in the background. We may realize that we don't have to create new trees or buildings and render them on the screen every time the character moves.
  - So, we create an instance of the tree first. Then we can create as many trees as we want from this instance (prototype) and update their positions. We may also choose to change the color of the trees for a new level in the game.
  - Instead of creating new objects, we just have to clone the prototypical instance.
- Example
  - suppose we have an Object that loads data from database. Now we need to modify this data in our program multiple times, so its not a good idea to create the Object using new keyword and load all the data again from database. 
  - So the better approach is to clone the existing object into a new object and then do the data manipulation.
- Prototype allows us to hide the complexity of making new instances from the client.
  - The concept is to copy an existing object rather than creating a new instance from scratch, something that may include costly operations
  - The existing object acts as a prototype and contains the state of the object. The newly copied object may change same properties only if required.
- Object pooling
-

## How

- using the clone() method. To do this, we'd implement the Cloneable interface.
  - When we're trying to clone, we should decide between making a shallow or a deep copy.
  -  if the class contains only primitive and immutable fields, we may use a shallow copy.
  - If it contains references to mutable fields, we should go for a deep copy. We might do that with copy constructors or serialization and deserialization.
- Parts
  - Prototype : This is the prototype of actual object.
  - Prototype registry : This is used as registry service to have all prototypes accessible using simple string parameters.
  - Client : Client will be responsible for using registry service to access prototype instances.

## When

- Prototype patterns is required, when object creation is time consuming, and costly operation, so we create object with existing object itself.
- When a system should be independent of how its products are created, composed, and represented and when the classes to instantiate are specified at run-time.
  - When instances of a class can have one of only a few different combinations of state. It may be more convenient to install a corresponding number of prototypes and clone them rather than instantiating the class manually, each time with the appropriate state.
  - By dynamic loading or To avoid building a class hierarchy of factories that parallels the class hierarchy of products


## Advantages

- when our new object is only slightly different from our existing one
  - instances may have only a few combinations of state in a class. So instead of creating new instances, we may create the instances with the appropriate state beforehand and then clone them whenever we want.
-  we might encounter subclasses that differ only in their state. We can eliminate those subclasses by creating prototypes with the initial state and then cloning them.
- This approach saves costly resources and time, especially when the object creation is a heavy process.
- Adding and removing products at run-time
  – Prototypes let you incorporate a new concrete product class into a system simply by registering a prototypical instance with the client.
  That’s a bit more flexible than other creational patterns, because a client can install and remove prototypes at run-time.
- Specifying new objects by varying values
  - Highly dynamic systems let you define new behavior through object composition by specifying values for an object’s variables and not by defining new classes.
- Specifying new objects by varying structure
  - Many applications build objects from parts and subparts. For convenience, such applications often let you instantiate complex, user-defined structures to use a specific subcircuit again and again.
- Reduced subclassing
  - Factory Method often produces a hierarchy of Creator classes that parallels the product class hierarchy. The Prototype pattern lets you clone a prototype instead of asking a factory method to make a new object. Hence you don’t need a Creator class hierarchy at all.


## Drawbacks

- Since we are cloning the objects, the process could get complex when there are many classes, thereby resulting in a mess. Additionally, it's difficult to clone classes that have circular references.
- Overkill for a project that uses very few objects and/or does not have an underlying emphasis on the extension of prototype chains.
- It also hides concrete product classes from the client
- Each subclass of Prototype must implement the clone() operation which may be difficult, when the classes under consideration already exist.
  - Also implementing clone() can be difficult when their internals include objects that don’t support copying or have circular references.

## Comparisons with other patterns

- Sometimes creational patterns are competitors:
  - there are cases when either Prototype or Abstract Factory could be used properly.
  - At other times they are complementary:
    - Abstract Factory might store a set of Prototypes from which to clone and return product objects.
    - Abstract Factory, Builder, and Prototype can use Singleton in their implementations.
- Abstract Factory classes are often implemented with Factory Methods, but they can be implemented using Prototype.
- Factory Method: creation through inheritance.
  - Prototype:
    - creation through delegation.
- Often, designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed.
- Prototype doesn't require subclassing, but it does require an "initialize" operation.
  - Factory Method requires subclassing, but doesn't require Initialize.
- Designs that make heavy use of the Composite and Decorator patterns often can benefit from Prototype as well.
- Prototype co-opts one instance of a class for use as a breeder of all future instances.
- Prototypes are useful when object initialization is expensive, and you anticipate few variations on the initialization parameters.
  - In this context, Prototype can avoid expensive "creation from scratch", and support cheap cloning of a pre-initialized prototype.
- Prototype is unique among the other creational patterns in that it doesn't require a class – only an object. Object-oriented languages like Self and Omega that do away with classes completely rely on prototypes for creating new objects.

## Links

- https://egkatzioura.com/2018/03/27/creational-design-patterns-prototype-pattern/
