# Classes

A class is a blueprint where objects can be created, an abstraction of all objects which are linked via behaviour and state.

For example, a dog is an abstraction of different dogs, like your aunt's dog Bubbles, or your neighbour' dog Rocky etc. Dog is the class, Bubbles and Rocky are the objects. Each dog has their own characteristics (ie state) and behaviour, but they are similar to each other. Bubbles and Rocky have state such as sex and age, which can be different. Dog has state such as sex and age which can take a range of values. Bubbles and Rocky have behaviour like bark and run, which can be different. Dog has behaviour such as bark and run, which can implement a common way of doing them that applies to all dogs.

- They can represent 
  - tangible things - wheel barrow
  - intangible things - checking account
  - ideas
  - processes
  - relationships
- They define behaviour of objects
- The get instantiated at runtime

```java
public class Dog {
    // These are the state, just fields
    private final Integer age;
    private final Sex sex;
    private final String name;
    private final Double maxSpeed;
    private final Breed breed;

    // See section about constructors here
    public Dog(Integer age, Sex sex, String name, Double maxSpeed, Breed breed) {
        this.age = age;
        this.sex = sex;
        this.name = name;
        this.maxSpeed = maxSpeed;
        this.breed = breed;
    }

    // These are the behaviours, just methods
    public String bark() {
        // implementation
    }

    public Double run(Double distance) {
        // implementation
    }

    // any more methods you want to access
}
```

## Links
