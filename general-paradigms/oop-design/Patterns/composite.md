# Composite Design Pattern

## What

- meant to allow treating individual objects and compositions of objects, or “composites” in the same way.
- is a partitioning design pattern and describes a group of objects that is treated the same way as a single instance of the same type of object
-  lets you compose objects into tree structures and then work with these structures as if they were individual objects.
- It can be viewed as a tree structure made up of types that inherit a base type, and it can represent a single part or a whole hierarchy of objects.
  - component
    - is the base interface for all the objects in the composition. It should be either an interface or an abstract class with the common methods to manage the child composites.
  - leaf
    - implements the default behavior of the base component. It doesn't contain a reference to the other objects.
  - composite/container
    -  has leaf elements. It implements the base component methods and defines the child-related operations.
    - is an element that has sub-elements: leaves or other containers.
    - Upon receiving a request, a container delegates the work to its sub-elements, processes intermediate results and then returns the final result to the client.
  - client
    - has access to the composition elements by using the base component object.
-

## When to use

- when the core model of your app can be represented as a tree.
- when you want the client code to treat both simple and complex elements uniformly.
- when clients need to ignore the difference between compositions of objects and individual objects.
- find that they are using multiple objects in the same way, and often have nearly identical code to handle each of them, then composite is a good choice, it is less complex in this situation to treat primitives and composites as homogeneous.

## Advantages

-  You can work with complex tree structures more conveniently: use polymorphism and recursion to your advantage
- You can introduce new element types into the app without breaking the existing code, which now works with the object tree.


## Drawbacks

- It might be difficult to provide a common interface for classes whose functionality differs too much. In certain scenarios, you’d need to overgeneralize the component interface, making it harder to comprehend.

## Comparisons with other patterns

- You can use Builder when creating complex Composite trees because you can program its construction steps to work recursively.
- Chain of Responsibility is often used in conjunction with Composite.
  - In this case, when a leaf component gets a request, it may pass it through the chain of all of the parent components down to the root of the object tree.
- You can use Iterators to traverse Composite trees.
- You can use Visitor to execute an operation over an entire Composite tree.
- You can implement shared leaf nodes of the Composite tree as Flyweights to save some RAM
- Composite and Decorator have similar structure diagrams since both rely on recursive composition to organize an open-ended number of objects.
  - A Decorator is like a Composite but only has one child component. There’s another significant difference: Decorator adds additional responsibilities to the wrapped object, while Composite just “sums up” its children’s results.
  - the patterns can also cooperate: you can use Decorator to extend the behavior of a specific object in the Composite tree.
- Designs that make heavy use of Composite and Decorator can often benefit from using Prototype. Applying the pattern lets you clone complex structures instead of re-constructing them from scratch.
