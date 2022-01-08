# Factory Pattern

- The Factory pattern allows client code to delegate creation of a particular kind of object to another class (“factory”).
  - The type of the returned instance can depend on some data supplied by the client or
  - can be based on the current context or state of the application.
- The factory method does not have to have any parameters passed to it, instead it may just examine the existing state of the application to make the decision

## Advantages

- decouples the calling class from the target class, which result in less coupled and highly cohesive code.
  - For example:
    - JDBC is a good example for this pattern; application code doesn’t need to know what database it will be used with, so it doesn’t know what database-specific driver classes it should use.
    - Instead, it uses factory methods to get Connections, Statements, and other objects to work with. Which gives you flexibility to change your back-end database without changing your DAO layer in case you are using ANSI SQL features and not coded on DBMS specific feature?
- enables the subclasses to provide extended version of an object, because creating an object inside factory is more flexible than creating an object directly in the client.
  - Since client is working on interface level any time you can enhance the implementation and return from Factory.
-  it encourages consistency in code since every time object is created using Factory rather than using different constructor at different client side.
- easy to debug and troubleshoot because you have a centralized method for object creation and every client is getting object from same place.
- Static factory method used in factory design pattern enforces use of Interface than implementation which itself is a good practice.
- Since factory method have return type as Interface, it allows you to replace implementation with better performance version in newer release.
- static factory method pattern is that they can cache frequently used object and eliminate duplicate object creation.
- offers alternative way of creating object.
- to hide information related to creation of object.



## See Wiring class

## DI library

## case swithc

## Supplier java 8

- https://dzone.com/articles/factory-pattern-using-lambda-expression-in-java-8
- https://programmingideaswithjake.wordpress.com/2015/01/31/making-simple-factories-via-lambdas/
- https://stackoverflow.com/questions/6606056/factory-design-pattern-not-use-static-methods-because-unit-testing-is-a-proble
- https://jaxenter.com/patterns-java-8-lambdas-127635.html
- https://stackoverflow.com/questions/23126207/what-is-the-most-effective-way-of-writing-a-factory-method
- https://stackoverflow.com/questions/29504945/the-best-way-to-implement-factory-without-if-switch
- https://dzone.com/articles/factory-pattern-using-lambda-expression-in-java-8

## Links

- https://egkatzioura.com/2018/03/27/creational-design-patterns-factory-pattern/
- https://www.jiffle.net/blog/2017/04/02/the-factory-pattern-using-java-8-lambda-evolved/
- https://dzone.com/articles/factory-method-vs-simple-factory-1
