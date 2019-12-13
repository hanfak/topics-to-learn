# Singleton

- A creational pattern, which onyl creates one and only one instance of a class. If instantiating another object, and an object already exists, it will return the object already created.
- This pattern involves a single class which is responsible for creating an object while making sure that only one object gets created.
- When you use this pattern, you define an object that will exist across all application scope and that you can easily access from anywhere in the code at any time
- Example

```java

class Singleton {
    private static Singleton INSTANCE = null;
    private String criticalData;
    // Any dependency in here
    private Singleton() {
        criticalData = "This should be unique and state should be universal";
    }

    synchronized static Singleton getInstance() {
        if (INSTANCE == null) {
            INSTANCE = new Singleton();
        }
        return INSTANCE;
    }
    public String getString() {
        return this.criticalData;
    }
}

```

- Example

```java
public class ASingleton {
    private static ASingleton _instance;

    private ASingleton() { }

    public static ASingleton Instance {
      if (_instance == null)
          _instance = new ASingleton();
      return _instance;
    }
}
```

## Why use Singleton

- If you have some resource that
  - (1) can only have a single instance, and
  - (2) you need to manage that single instance,
  - Examples
    - Logs
      - but it can be passed in as a dependency for each class
    - Database/connection pool
    - Properties
- A Singleton candidate must satisfy three requirements:
    - controls concurrent access to a shared resource.
    - access to the resource will be requested from multiple, disparate parts of the system.
    - there can be only one object.
  - If not all are satisfied, should redesign
- A singleton should be used when managing access to a resource which is shared by the entire application, and it would be destructive to potentially have multiple instances of the same class. Making sure that access to shared resources thread safe is one very good example of where this kind of pattern can be vital.

## Disadvantages of Singleton

 - Using synchronized, a synchronized block can be accessed one thread at a time, this might create a bottleneck for even getting the instance of the object.
 - Unit testing
   - One of the major requirements of unit testing is that each test should be independent of others. This can cause tests to pass when, really, it's because they were called in a particular order
     - They carry state around for the lifetime of the application
   - They inherently cause code to be tightly coupled. This makes faking them out under test rather difficult in many cases.
 - Breaks Single Responsibility Principle
   -  a class should not know whether it is a singleton or not. So if you want to limit the ability to instantiate, use the factory or builder patterns, which encapsulates creation. There, you can limit the number of objects to one or whatever you wish for.
 - Singletons Provide Global State
   - Because you hide the dependencies of your application in your code, instead of exposing them through the interfaces. Making something global to avoid passing it around is a code smell.
