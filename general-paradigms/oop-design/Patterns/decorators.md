# Decorator Pattern

- The Decorator pattern allows the addition of behaviour to existing classes without changing the original class
- The pattern also allows the “wrapping” of multiple decorators inside each other to compose behaviours.
  - Thus delegating behaviour to the wrapped object
- Implements open/closed principle
- The decorator pattern typically starts with an abstraction of some behaviour.
- A decorator implements the same interface as the class it is decorating. It also contains a reference to the decorated (“wrapped”) instance.
- The decorator delegates to the “wrapped” instance of a decorator
- The key thing here is that extra runtime behaviour has been added without having to modify the original class
- keep software soft because existing behaviour can be extended and composed without having to change existing implementation code
- Decorator works best when you have just a single I/O channel...[it] is a great way to allow to dynamically compose the way we apply processing to it.

## How

- You start with an interface which creates a blue print for the class which will have decorators.
- Then implement that interface with basic functionalities.
- Till now we have got an interface and an implementation concrete class.
- Create an abstract class that contains an attribute type of the interface. The constructor of this class assigns the interface type instance to that attribute. This class is the decorator base class.
- Now you can extend this class and create as many concrete decorator classes. The concrete decorator class will add its own methods. After / before executing its own method the concrete decorator will call the base instance’s method.
- Key to this decorator design pattern is the binding of method and the base instance happens at runtime based on the object passed as parameter to the constructor. Thus dynamically customizing the behavior of that specific instance alone.

## When

- For responsibilities that can be withdrawn
- When extension by sub-classing is impractical.
  - Sometimes, a large number of independent extensions are possible and would produce an explosion of subclasses to support every combination.
  - Class definition may be hidden or otherwise unavailable for sub-classing.

## Advantages

- Decorator Pattern is flexible than inheritance because inheritance add responsibilities at compile time and it will add at run-time.
- Decorator pattern enhance or modify the object functionality

## Drawbacks

- Main disadvantage of using Decorator Pattern in Java is that the code maintenance can be a problem as it provides a lot of similar kind of small objects (each decorator).

## Comparison with other design Patterns

- Adapter provides a different interface to its subject. Proxy provides the same interface.
  - Decorator provides an enhanced interface.
- Adapter changes an object’s interface,
  - Decorator enhances an object’s responsibilities.
  - Decorator is thus more transparent to the client. As a consequence, Decorator supports recursive composition, which isn’t possible with pure Adapters.
- Composite and Decorator have similar structure diagrams, reflecting the fact that both rely on recursive composition to organize an open-ended number of objects.
- A Decorator can be viewed as a degenerate Composite with only one component.
  - However, a Decorator adds additional responsibilities – it isn’t intended for object aggregation.
- Decorator is designed to let you add responsibilities to objects without subclassing.
  - Composite’s focus is not on embellishment but on representation. These intents are distinct but complementary.
  - Consequently, Composite and Decorator are often used in concert.
- Composite could use Chain of Responsibility to let components access global properties through their parent.
  - It could also use Decorator to override these properties on parts of the composition.
- Decorator and Proxy have different purposes but similar structures.
  - Both describe how to provide a level of indirection to another object, and the implementations keep a reference to the object to which they forward requests.
- Decorator lets you change the skin of an object.
  - Strategy lets you change the guts.

## Link

- https://www.yegor256.com/2015/02/26/composable-decorators.html
