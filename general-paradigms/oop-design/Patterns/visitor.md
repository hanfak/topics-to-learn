# Visitor Pattern

In object-oriented programming and software engineering, the visitor design pattern is a way of separating an algorithm from an object structure on which it operates. A practical result of this separation is the ability to add new operations to existing object structures without modifying those structures. It is one way to follow the open/closed principle.

We could use inheritance to do this, but it will mean that each object will need to be modified (OCP)

### Links

- https://softwareengineering.stackexchange.com/questions/333692/understanding-the-need-of-visitor-pattern
- https://medium.com/factory-mind/visitor-design-pattern-demystified-940bd3903d56
- http://webcache.googleusercontent.com/search?q=cache:http://butunclebob.com/ArticleS.UncleBob.IuseVisitor
- https://www.codeproject.com/Articles/872151/Visitor-Pattern-ReExplained
- https://www.journaldev.com/1769/visitor-design-pattern-java
- https://stackoverflow.com/questions/9759141/overloading-in-java-and-multiple-dispatch

## Generified visitor

https://stackoverflow.com/questions/36363142/generified-implementation-of-visitor-pattern-in-java

## Double dispatch

- dynamic dispatch. The actual implementation of a method is selected in runtime by the target object
    ```java
    interface Greetings {
      void hello();
    }

    class Foo extends Greetings {
      public void hello() { System.out.println("Hello"); }
    }

    class Bar extends Greetings {
      public void hello() { System.out.println("Hi!"); }
    }

    Greetings g = /* ... */;
    g.hello();
    ```
- Double ouble dispatch
  -  The ability to choose the method implementation based on this object and also one of the arguments passed to the function.
  - the Visitor pattern is a way to simulate the lack of support for double dispatch
- To simulate multiple dispatch is a language feature known as pattern matching.

## Anti patern

- https://typeinference.com/oop/2015/08/17/anti_oop_design_patterns.html
