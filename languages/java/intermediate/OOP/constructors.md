# Constructors

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Constructors](#constructors)
	- [What](#what)
	- [Default/hidden constructor](#defaulthidden-constructor)
	- [Paramatised constructor](#paramatised-constructor)
	- [Overlaoding](#overlaoding)
	- [Private constructors](#private-constructors)
	- [Telescoping](#telescoping)
	- [Static initialization/ static factory methods](#static-initialization-static-factory-methods)
	- [initialization Block](#initialization-block)
		- [Links](#links)
	- [Dealing with Dependency injection frameworks](#dealing-with-dependency-injection-frameworks)

<!-- /TOC -->

## What

- It is a public method, with same name and case as the class. It is invoke when newing up an instance of the class.
- Constructors should do one thing, just set the fields of the object to the arguments passed in via the constructor


## Default/hidden constructor

- a constructor that is created by the java if none is provided.
- Can provide one but it will be there at compile time

  ```java
  class Dog {
    public Dog(){} //default constructor
  }
  ```
- https://stackoverflow.com/questions/4488716/java-default-constructor


## Paramatised constructor

- A constructor that has parameters
  ```java
  class Dog {
    public Dog(Integer age){}
  }
  ```
  - Noramlly set age to some field in the class.
- Parameters are generally set to fields of the objects
  ```java
  class Dog {
    private final Integer age = age;

    public Dog(Integer age){
      this.age = age;
    }
  }
  ```
- Parameters are normally the dependencies of the object, and used with in the instance methods to delegate behaviour to them.
  ```java
  class Dog {
    private final Breed breed = breed;

    public Dog(Integer breed){
      this.breed = breed;
    }

    public Double run(Double distance) {
      return distance / breed.getMaxSpeed()
    }
  }
  ```
  ## this

  - this.age refers to the object's field, where age is what is pass in to the method via arguments.
  - `this` on its own refers to the object, thus calling `this.run()` means calling the objects own `run()` method which will use its own instnace fields
    - we dont need to use `this.run()`, when call another method within an class, which just call `run()`, as it is implicit implied.

## Overlaoding

- Having many constructors, with different parameter list
- Allows for default certain fields or parameters

```java
class Dog {
  private final Integer age = age;

  public Dog(){
    this.age = 2;
  }

  public Dog(Integer age){
    this.age = age;
  }
}
```

```java
Dog dog1 = new Dog(); // will have age = 2
Dog dog2 = new Dog(5); // will have age = 5
```

-  explicit constructor invocation
```java
class Dog {
  private final Integer age = age;
  private final String name = name;

  public Dog(){
    this(2, "Rocky");
  }

  public Dog(Integer age){
    this(age, "Rocky");
  }

  public Dog(Integer age, String name){
    this.age = age;
    this.namr = name;
  }
}
```
```java
Dog dog1 = new Dog(); // will have age = 2, name = Rocky
Dog dog2 = new Dog(5); // will have age = 5, name= Rocky
Dog dog4 = new Dog(5, "Bubbles"); // will have age = 5, name= Bubbles
```

- Using `this` in telescoping constructors (see overloading)


## Private constructors

- Used for not allow other objects to instantiate an object, only class can do this.
- Used in general for static factory methods (see below)
- exanple ?????

## Telescoping

- lots of constructors, as there are lots of fields and want defaults for different versions of the class
- Use of builder pattern or static factory method
- https://www.vojtechruzicka.com/avoid-telescoping-constructor-pattern/

## Static initialization/ static factory methods

- Useful for creating new domain objects
- Useful for adding code (ie validation), setting fields as null or defaults
- Better naming
- example
  ```java
  public class Card {
      public final Rank rank;
      public final Suit suit;

      private Card(Rank rank, Suit suit) {
          this.rank = rank;
          this.suit = suit;
      }

      public static Card card(Rank rank, Suit suit) {
          return new Card(rank, suit);
      }
  }
  ```
- https://stackoverflow.com/questions/929021/what-are-static-factory-methods
- Negatives
	- no inheritance

## initialization Block

### Links

- https://docs.oracle.com/javase/tutorial/java/javaOO/constructors.html
- https://www.javatpoint.com/java-constructor

## Dealing with Dependency injection frameworks

- Due to Most DI using reflection, factories might not be possible, and constructors might need to be polluted with logic
