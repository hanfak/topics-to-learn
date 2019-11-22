# Enums

A list of ordered named constants. The constants are of type of that enum type. Cannot instantiate enum type.

```java
public enum Direction {
  EAST, SOUTH, WEST, NORTH // Generally all capitals
}
```

To use an enum:

```java
Direction aDirection = Direction.EAST;
```
  - Notice the type of aDirection is the enum type, Direction.
  - To use enum, use it like static/class field

Use of ordinals.

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

Implementing an inteface

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

Enum methods

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
