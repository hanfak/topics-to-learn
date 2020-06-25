# 4. Interface Segregation Principle

- It leads to the development of a greater number of more highly cohesive interfaces, rather than fewer bigger and bloated ones.
-  the class implementing the interface should not have to implement lots of things that it does not care about; it should only have to implement the things it needs.
- SRP for interfaces

why?
- A class can choose to implement IPrintable and IRotatable but does not have to implement anything else (such as ISizeable). If there was only one interface (such as IShapeOperations) that contained printing, rotating and sizing, a client class could not just implement printing on its own.
- 

## Links

- https://stackify.com/interface-segregation-principle/
- https://dzone.com/articles/solid-principles-interface-segregation-principle
