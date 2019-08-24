# Encapsulation

## Definitions


- Encapsulation is a programming language feature.
- Encapsulation means drawing a boundary around something. It means being able to talk about the inside and the outside of it
- an object being strongly or weakly encapsulated depending on how much of its implementation is hidden.
- Encapsulation allows you to check access to your own innards, and provide specific methods of performing such access
  -  It does not specifically address leaking implementation details; although you can control access to that variable, you can no longer control the fact that the client knows your using an ArrayList, even if you later decide to use LinkedList.
- Encapsulation is the grouping of related ideas into one unit, which can thereafter be referred to by a single name.
  - attributes that represents the state of an object and the methods that work on them are packaged into an object type.
- The result of hiding a representation and implementation in an object...
- Encapsulation is an OOP concept where object state(class fields) and it's behaviour(methods) is wrapped together. Java provides encapsulation using class.

## Information hiding

- Information Hiding is a design principle
  - use interfaces rather than objects (other than at creation).
- information hiding gives rise to the notions of encapsulation and abstraction.
- every module in the [...] decomposition is characterized by its knowledge of a design decision which it hides from all others. Its interface or definition was chosen to reveal as little as possible about its inner workings.
  - some separate entity or module which has some responsibility that we need fulfilled, and we are not interested about how it is fulfilled. But the emphasis here is a bit more about hiding the details from other modules (or objects)
- InformationHiding is the idea that a design decision should be hidden from the rest of the system to prevent unintended coupling
- is hiding the fact that your using an ArrayList to implement your data structure. Although the client could still find out how your implementing it (Information Hiding Is Not Information Erasing), you're no longer responsible for supporting that implementation.
- mechanism for restricting access to some of the object's components. Your above example is the case of Information Hiding if you make age private.

## Encapsulation is not information hiding

- Information Hiding should inform the way you encapsulate things, but of course it doesn't have to
- encapsulation does need some degree of information hiding.

- https://www.javaworld.com/article/2075271/core-java/encapsulation-is-not-information-hiding.html
- http://web.archive.org/web/20000816234125/http://www.itmweb.com:80/essay550.htm
- http://web.archive.org/web/20090505194203/http://homepage.mac.com/keithray/blog/2006/02/22/#EncapsulationHiding
- http://wiki.c2.com/?EncapsulationIsNotInformationHiding
- http://www.stefanoricciardi.com/2009/12/06/encapsulation-and-information-hiding/
