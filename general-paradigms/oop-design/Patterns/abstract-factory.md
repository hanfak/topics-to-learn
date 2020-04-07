# abstract Factory

## What

- This pattern is one level of abstraction higher than factory pattern. This means that the abstract factory returns the factory of classes.
- Like Factory pattern returned one of the several sub-classes, this returns such factory which later will return one of the sub-classes.

## Advantages

- it isolates the concrete classes that are generated. The names of actual implementing classes are not needed to be known at the client side. Because of the isolation, you can change the implementation from one factory to another.

## When to use

- A system should be independent of how its products are created, composed, and represented
- A class can’t anticipate the class of objects it must create
- A system must use just one of a set of families of products
- A family of related product objects is designed to be used together, and you need to enforce this constraint

## Other

- Abstract Factory, Builder, and Prototype can use Singleton in their implementation. Abstract Factory Pattern is often used along with Factory Method but also can be implemented using Prototype pattern to increase the performance and simplifying the code.
- Abstract Factory can be used as an alternative to Façade pattern to hide platform specific classes
- AbstractFactory class declares only an interface for creating the products. The actual creation is the task of the ConcreteProduct classes, where a good approach is applying the Factory Method design pattern for each product of the family.

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
