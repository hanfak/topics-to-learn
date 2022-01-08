# abstract Factory

## What

- This pattern is one level of abstraction higher than factory pattern. This means that the abstract factory returns the factory of classes.
- Like Factory pattern returned one of the several sub-classes, this returns such factory which later will return one of the sub-classes.
- provides an interface for creating families of related or dependent objects without specifying their concrete classes
  - create objects that follow a general pattern

## Advantages

- it isolates the concrete classes that are generated. The names of actual implementing classes are not needed to be known at the client side. Because of the isolation, you can change the implementation from one factory to another.
  - The Abstract Factory pattern helps you control the classes of objects that an application creates. Because a factory encapsulates the responsibility and the process of creating product objects, it isolates clients from implementation classes. Clients manipulate instances through their abstract interfaces. Product class names are isolated in the implementation of the concrete factory; they do not appear in client code.
- Exchanging Product Families easily: The class of a concrete factory appears only once in an application, that is where it’s instantiated. This makes it easy to change the concrete factory an application uses. It can use various product configurations simply by changing the concrete factory. Because an abstract factory creates a complete family of products, the whole product family changes at once.
- Promoting consistency among products: When product objects in a family are designed to work together, it’s important that an application use objects from only one family at a time. AbstractFactory makes this easy to enforce.

##  Drawbacks

- While the pattern is great when creating predefined objects, adding the new ones might be challenging
- Difficult to support new kind of products: Extending abstract factories to produce new kinds of Products isn’t easy. That’s because the AbstractFactory interface fixes the set of products that can be created. Supporting new kinds of products requires extending the factory interface, which involves changing the AbstractFactory class and all of its subclasses.

## How

- The client code calls the creation methods of a factory object instead of creating products directly with a constructor call (new operator). Since a factory corresponds to a single product variant, all its products will be compatible.
- Client code works with factories and products only through their abstract interfaces. It allows the same client code to work with different products. You just create a new concrete factory class and pass it to the client code.
- Components
  - AbstractFactory : Declares an interface for operations that create abstract product objects.
  - ConcreteFactory : Implements the operations declared in the AbstractFactory to create concrete product objects.
  - Product : Defines a product object to be created by the corresponding concrete factory and implements the AbstractProduct interface.
  - Client : Uses only interfaces declared by AbstractFactory and AbstractProduct classes.

## When to use

- A system should be independent of how its products are created, composed, and represented
- A class can’t anticipate the class of objects it must create
- A system must use just one of a set of families of products
- A family of related product objects is designed to be used together, and you need to enforce this constraint
- The client is independent of how we create and compose the objects in the system
- The system consists of multiple families of objects, and these families are designed to be used together
- We need a run-time value to construct a particular dependency

## Other

- Abstract Factory, Builder, and Prototype can use Singleton in their implementation. Abstract Factory Pattern is often used along with Factory Method but also can be implemented using Prototype pattern to increase the performance and simplifying the code.
- Abstract Factory can be used as an alternative to Façade pattern to hide platform specific classes
- AbstractFactory class declares only an interface for creating the products. The actual creation is the task of the ConcreteProduct classes, where a good approach is applying the Factory Method design pattern for each product of the family.
- Sometimes creational patterns are competitors: there are cases when either Prototype or Abstract Factory could be used profitably. At other times they are complementary:
  - Abstract Factory might store a set of Prototypes from which to clone and return product objects, Builder can use one of the other patterns to implement which components get built. Abstract Factory, Builder, and Prototype can use Singleton in their implementation.
- Abstract Factory, Builder, and Prototype define a factory object that's responsible for knowing and creating the class of product objects, and make it a parameter of the system.
  - Abstract Factory has the factory object producing objects of several classes. Builder has the factory object building a complex product incrementally using a correspondingly complex protocol. Prototype has the factory object (aka prototype) building a product by copying a prototype object.
- Abstract Factory classes are often implemented with Factory Methods, but they can also be implemented using Prototype.
- Abstract Factory can be used as an alternative to Facade to hide platform-specific classes.
- Builder focuses on constructing a complex object step by step. Abstract Factory emphasizes a family of product objects (either simple or complex). Builder returns the product as a final step, but as far as the Abstract Factory is concerned, the product gets returned immediately.

## Difference between Abstract Factory and Factory Method pattern

- Factory Method pattern exposes a method to the client for creating the object
  -  Abstract Factory they expose a family of related objects which may consist of these Factory methods.
- Designs start out using Factory Method (less complicated, more customizable, subclasses proliferate) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, more complex) as the designer discovers where more flexibility is needed.
- Factory Method pattern hides the construction of single object where as abstract factory method hides the construction of a family of related objects. Abstract factories are usually implemented using (a set of) factory methods.

## Links

- https://codurance.com/2015/04/14/design-patterns-in-the-21st-century-part-two/
- https://github.com/promiennam/design-pattern/tree/master/src/promiennam/designpattern/abstractfactory

## abstract factory using enums

faster then using if/else

- https://stackoverflow.com/questions/21811665/creating-object-from-enum-reference
- https://www.javacodegeeks.com/2013/06/factory-design-pattern-an-effective-approach.html
