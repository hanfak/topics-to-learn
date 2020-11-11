# Singleton


<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Singleton](#singleton)
	- [What](#what)
	- [Why use Singleton](#why-use-singleton)
	- [Disadvantages of Singleton](#disadvantages-of-singleton)
	- [Links](#links)

<!-- /TOC -->

## What

- A creational pattern, which only creates one and only one instance of a class. If instantiating another object, and an object already exists, it will return the object already created.
- This pattern involves a single class which is responsible for creating an object while making sure that only one object gets created.
- When you use this pattern, you define an object that will exist across all application scope and that you can easily access from anywhere in the code at any time
- Sometimes it is necessary that one and only one instance of a particular class exists in the entire Java Virtual Machine.  This is achieved through the Singleton design pattern
- The singleton class must provide a global access point to get the instance of the class.


### Example

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

### Example

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
		- caching
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

## Types

### Lazy initialization

- The Singleton pattern is implemented by creating a class with a method that creates a new instance of the object if one does not exist.
- If an instance already exists, it simply returns a reference to that object.
- To make sure that the object cannot be instantiated any other way, the constructor is made private.
- Although a Singleton can be implemented as a static instance, it can also be lazily constructed, requiring no memory or resources until needed.
-  works fine in case of the single-threaded environment but when it comes to multithreaded systems, it can cause issues if multiple threads are inside the if condition at the same time

```java
public class LazyInitializedSingleton {

    private static LazyInitializedSingleton instance;

    private LazyInitializedSingleton(){}

    public static LazyInitializedSingleton getInstance(){
        if(instance == null){
            instance = new LazyInitializedSingleton();
        }
        return instance;
    }
}
```

### Thread Safe

-  is to make the global access method synchronized, so that only one thread can execute this method at a time.
- provides thread-safety but it reduces the performance because of the cost associated with the synchronized method, although we need it only for the first few threads who might create the separate instances

```java
public class ThreadSafeSingleton {

    private static ThreadSafeSingleton instance;

    private ThreadSafeSingleton(){}

    public static synchronized ThreadSafeSingleton getInstance(){
        if (instance == null) {
            instance = new ThreadSafeSingleton();
        }
        return instance;
    }

}
```

### Lazy initialization with Double check locking

- The above works absolutely fine in a single threaded environment and processes the result faster because of lazy initialization.
- However the above code might create some abrupt behavior in the results in a multithreaded environment as in this situation multiple threads can possibly create multiple instance of the same SingletonExample class if they try to access the getSingletonInstance() method at the same time.
- In the multithreading environment to prevent each thread to create another instance of singleton object and thus creating concurrency issue we will need to use locking mechanism.
	- This can be achieved by synchronized keyword. By using this synchronized keyword we prevent Thread2 or Thread3 to access the singleton instance while Thread1 is inside the method getSingletonInstance().
	- So this means that every time the getSingletonInstance() is called it gives us an additional overhead. To prevent this expensive operation we will use double checked locking so that the synchronization happens only during the first call and we limit this expensive operation to happen only once.
- Issues:
	- http://www.cs.umd.edu/~pugh/java/memoryModel/DoubleCheckedLocking.html

```java
public class ThreadSafeSingleton {

    private static volatile ThreadSafeSingleton instance;

    private ThreadSafeSingleton(){}

		public static ThreadSafeSingleton getInstanceUsingDoubleLocking(){
		    if (instance == null) {
		        synchronized (ThreadSafeSingleton.class) {
		            if (instance == null) {
		                instance = new ThreadSafeSingleton();
		            }
		        }
		    }
		    return instance;
		}

}
```


### Eager initialization

- If the program will always need an instance, or if the cost of creating the instance is not too large in terms of time/resources, the programmer can switch to eager initialization, which always creates an instance when the class is loaded into the JVM.
- But in most of the scenarios, Singleton classes are created for resources such as File System, Database connections, etc. We should avoid the instantiation until unless client calls the getInstance method

```java
public class EagerInitializedSingleton {

    private static final EagerInitializedSingleton instance = new EagerInitializedSingleton();

    //private constructor to avoid client applications to use constructor
    private EagerInitializedSingleton(){}

    public static EagerInitializedSingleton getInstance(){
        return instance;
    }
}
```

### Static block initialization

- This is similar to the eager initialization.
- The main advantage of using the static block here is that it supports the options for exception handling for the instantiation of the singleton class.

```java
public class StaticBlockSingleton {

    private static StaticBlockSingleton instance;

    private StaticBlockSingleton(){}

    //static block initialization for exception handling
    static{
        try{
            instance = new StaticBlockSingleton();
        }catch(Exception e){
            throw new RuntimeException("Exception occured in creating singleton instance");
        }
    }

    public static StaticBlockSingleton getInstance(){
        return instance;
    }
}
```

### Using Enum

- Enum has some distinct benefits in terms of thread-safety during instance creation, serialization guarantee by JVM and amazingly reduce amount of code which makes it perfect choice of using as Singleton class.
- Protects against reflection
- only limitation is that they are only eagerly instantiated.

```java
enum Singleton {
    INSTANCE;

    private Singleton() {
        System.out.println("Instance Created");
    }
}
```

###  Initialization-on-demand holder idiom (Bill Pugh)

- This idiom derives its thread safety from the fact that operations that are part of class initialization, which is guaranteed by the JVM.
- It derives its lazy initialization from the fact that the inner class is not loaded until some thread references one of its fields or methods. This provides the best of both options and guaranteed to be thread-safe by the JVM.
- The trick is to use private nested class to hold Singleton instance.
- Singleton class using an inner static helper class.
-  When the singleton class is loaded, SingletonHelper class is not loaded into memory and only when someone calls the getInstance method, this class gets loaded and creates the Singleton class instance
- doesn’t require synchronization

```java
public class BillPughSingleton {

    private BillPughSingleton(){}

    private static class SingletonHelper{
        private static final BillPughSingleton INSTANCE = new BillPughSingleton();
    }

    public static BillPughSingleton getInstance(){
        return SingletonHelper.INSTANCE;
    }
}
```

### Cloning

- Cloning the object can still copy it and result into duplicate object.
- The clone of the singleton object can be constructed using clone() method of the object.
- Hence it is advisable to overload clone() method of Object class and throw CloneNotSupportedException exception.

```java
public class CloneProofSingleton implements Cloneable {

    private static CloneProofSingleton instance;

    private CloneProofSingleton() {}

    public static synchronized CloneProofSingleton getInstance() {
        if (instance == null){
            instance = new CloneProofSingleton();
        }

        return instance;
    }

    //Prevents singleton instance from cloning
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return getInstance();

        //or else throw new CloneNotSupportedException()
    }
}
```

### Protecting against reflection

- Reflection API is a powerful API in java which can be used to instantiate any class even the class has private constructors. This will break the singleton design pattern.
- To prevent your singleton from Reflection API, just throw an IllegalStateException from private constructor if anybody tries to create a second instance

```java
public class ReflectionProofSingleton {

		private static final ReflectionProofSingleton instance = new ReflectionProofSingleton();

    private ReflectionProofSingleton() {
        if (instance != null) {
            throw new IllegalStateException("Instance already created");
        }
    }

    public static ReflectionProofSingleton getInstance() {
        return instance;
    }
}
```

### Protecting Singleton From Deserialization

- We frequently serialize and de-serialize the objects in Java. You know that de-serialization always creates a new instance of the class. This may destroy your singleton pattern.
- To protect the singleton from de-serialization, you have to implement readResolve() method in your singleton class. It is called when the object is de-serialized.

```java
public class DeserializationProofSingleton implements Serializable {

    private static DeserializationProofSingleton instance;

    private DeserializationProofSingleton() {}

    public static synchronized DeserializationProofSingleton getInstance() {
        if (instance == null){
            instance = new DeserializationProofSingleton();
        }
        return instance;
    }

    // readResolve() method : returns the existing instance
    protected Object readResolve() {
        return instance;
    }
}
```

## Singleton vs Static classes

- The Singleton pattern has several advantages over static classes.
	- a singleton can extend classes and implement interfaces, while a static class cannot (it can extend classes, but it does not inherit their instance members)
	- A singleton can be initialized lazily or asynchronously while a static class is generally initialized when it is first loaded, leading to potential class loader issues.
	- singletons can be handled polymorphically without forcing their users to assume that there is only one instance.
- When to use static classes
	- Prime example of this is java.lang.Math which is not Singleton, instead a class with all static methods.
	- If your Singleton is not maintaining any state, and just providing global access to methods, than consider using static class, as static methods are much faster than Singleton, because of static binding during compile time.
		-  But remember its not advised to maintain state inside static class, especially in concurrent environment, where it could lead subtle race conditions when modified parallel by multiple threads without adequate synchronization
	- You can also choose to use static method, if you need to combine bunch of utility method together.
		- Anything else, which requires singles access to some resource, should use Singleton design pattern.

## Links

- https://egkatzioura.com/2018/03/27/creational-design-patterns-singleton-pattern/
- https://javarevealed.wordpress.com/2013/07/04/singleton-design-pattern/
- https://shipilev.net/blog/2014/safe-public-construction/
