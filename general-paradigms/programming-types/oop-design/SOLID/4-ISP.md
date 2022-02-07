# 4. Interface Segregation Principle

- It leads to the development of a greater number of more highly cohesive interfaces, rather than fewer bigger and bloated ones.
-  the class implementing the interface should not have to implement lots of things that it does not care about; it should only have to implement the things it needs.
- SRP for interfaces
- You done want to be in situation where a class does alot things, so the consumer of the class only needs to use part of that class
  - this can lead shard behaviour with the class, which can impact other consumers for no reason. As one class could impact another.

why?
- A class can choose to implement IPrintable and IRotatable but does not have to implement anything else (such as ISizeable). If there was only one interface (such as IShapeOperations) that contained printing, rotating and sizing, a client class could not just implement printing on its own.
-

## ISsues

- segregating interfaces is a technique to reduce coupling and increase cohesion, however it can also reduce cohesion if carried to the extreme. Don’t always do it. Focus on balancing the cohesion and coupling in your system.
  - Have one interface cnotain one method, and having class implement several interfaces lead to explosion of classes and names
  - Reduces cohesion, as if you put one interface to a class, then logic is split out

### Links
- https://naildrivin5.com/blog/2019/11/21/interface-segreation-principle-is-unhelpful-but-inoffensive.html

## Links

- https://stackify.com/interface-segregation-principle/
- https://dzone.com/articles/solid-principles-interface-segregation-principle
