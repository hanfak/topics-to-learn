# Enums

A list of ordered named constants. The constants are of type of that enum type. Cannot instantiate enum type.

```java
public enum Direction {
  EAST, SOUTH, WEST, NORTH // Generally all capitals
}
```

## When to use

- When you need a predefined list of values which do represent some kind of numeric or textual data, you should use an enum
- You should always use enums when a variable (especially a method parameter) can only take one out of a small set of possible values.
  - constants or flags
- If you use enums instead of integers (or String codes), you increase compile-time checking and avoid errors from passing in invalid constants, and you document which values are legal to use.

## Properties

- an enum cannot extend anything else.
- Enum in Java are type-safe: Enum has there own name-space. It means your enum will have a type for example EAST in above example and you can not assign any value other than specified in Enum Constants.
  - ```Direction east = Direction.EAST;```
  - ```Direction east = 1; // Compile error```
- Enum constants are implicitly static and final and can not be changed once created.
- Enum can be safely compare using
  - Switch-Case Statement
  - == Operator
  - .equals() method
- You can not create instance of enums by using new operator in Java because constructor of Enum in Java can only be private and Enums constants can only be created inside Enums itself.
- Instance of Enum in Java is created when any Enum constants are first called or referenced in code.
- An enum specifies a list of constant values assigned to a type.
- An enum can be declared outside or inside a class, but NOT in a method.
- An enum declared outside a class must NOT be marked static, final , abstract, protected , or private
- Enums can contain constructors, methods, variables, and constant class bodies.
- enum constants can send arguments to the enum constructor, using the syntax BIG(8), where the int literal 8 is passed to the enum constructor.
- enum constructors can have arguments, and can be overloaded.
- enum constructors can NEVER be invoked directly in code. They are always called automatically when an enum is initialized.
- The semicolon at the end of an enum declaration is optional.



## To use an enum:

```java
Direction aDirection = Direction.EAST;
```
  - Notice the type of aDirection is the enum type, Direction.
  - To use enum, use it like static/class field

## Use of ordinals.

```java
int orderValueInEnum = direction.WEST.ordinal();
//returns 2
```
  - Starts list at 0, like arrays
  - Avoid using ordinals, unless certain that the enum list will not be added to. (see effective java)

toString() and getName()

```java
System.out.println(direction.WEST); // prints WEST

String nameOfEnum = direction.WEST.name() // returns  WEST
```

## Implementing an inteface

```java
interface Laugh {
    String execute();
}

enum Gender implements Laugh {
    FEMALE {
        @Override
        public String execute() {
            return "HA HA";
        }
    },
    MALE {
        @Override
        public String execute() {
            return "Ho HO";
        }
    };

    public abstract String execute();
}

for (Laugh cmd : Gender.values()) {
    System.out.println(cmd.execute());
}
```
  - When defining method in block, must also define it as abstract singature of method outside of block
  - Do not need to have interface to define method in block

## Enum methods

 - enum type is actually a class type
 - compiler creates class of this enum
   - can have fields, constructors and methods
   - the class extends java.lang.Enum which has toSting(), equals() etc
 - The power of this way, is to avoid using decision/control statements and use polymorphism to implement the logic based on the enum type without having to know about the enum type
   - Benefit: reduce code bloat in calling code
   - Benefit: only one place to change logic or add new types, instead of in the calling class

```java
public enum Level {
  LOW(30), MEDIUM(15), HIGH(7), URGENT(1);

  // Declare an instance variable
  private int levelValue;

  // Declare a private constructor
  private Level(int levelValue) {
    this.levelValue = levelValue;
  }

  public int getLevelValue() {
    // This can have other logic, can use params passed into this method to
    return levelValue;
  }
}

int levelValue = Level.LOW.getLevelValue();
//returns 30
```

## Singleton

```java

public enum MySingleton {
     INSTANCE;
     public void someMethod() { ... }
}

```

Actually equivalent to;

```java
public final class MySingleton {
    public final static MySingleton INSTANCE = new MySingleton();
    private MySingleton(){}
    public void someMethod() { ... }
}


// When your code first accesses INSTANCE, the class MySingleton will be loaded and initialized by the JVM. This process initializes the static field above once (lazily).
```

### Why is it better?

- it is more concise,
- provides the serialization machinery for free,
- provides an ironclad guarantee against multiple instantiation, even in the face of sophisticated serialization or reflection attacks
