### Static VS Instance

- Static keyword in Java is used for memory management.
  - used for keeping the same copy of variables or methods for every instance of a class
  - If a member of a class is static, it can be accessed before any objects are created for that class and also without any object reference.

## Static vs Non-Static variables

- If a field has the same value for all instances, it should be static
  - beacuse  its a wastage of memory as for each object created it would allocate memory for that field variable for each of the instances created and further assign the given value in it.
- As a static variable, it would independent of the no. of instances created thereby saving memory.

## Static vs Non-Static Methods

- Static methods are utility methods in a class which can be exposed to other classes without having to create an instance of the owner class to call the method.
- static methods are less memory intensive compared to non-static methods
- a non-static method is an instance-based method that needs to be called by specific instances of the class and the behavior of such methods completely depends on the state of the objects which calls them.
- Also used for factory methods
- Difference
  - Access
    - A static method can access only static members and can not access non-static members.
    - A non-static method can access both static as well as non-static members.
  - Binding
    - Static method uses complie time binding or early binding.
    - Non-static method uses run time binding or dynamic binding.
  - Overriding
    - A static method cannot be overridden being compile time binding.
    - A non-static method can be overridden being dynamic binding.
  - Memory allocation
    - Static method occupies less space and memory allocation happens once.
    - A non-static method may occupy more space. Memory allocation happens when method is invoked and memory is deallocated once method is executed completely.
  - Keyword
    - A static method is declared using static keyword.
    - A normal method is not required to have any special keyword.

## Static Initialization block vs initialization block

- a block is a set of statements enclosed within curly braces which are used as a compound statement or a single unit of code.
- used in Methods, if-else statements, loops, and lambdas,
- blocks which are not used by other Java constructs are Independent blocks
  - are broad of two types namely
    - static initializer blocks
      - static keyword is used to define a static initialization block.
      - gets loaded as soon as a class gets loaded in the memory and is not associated with a call to the constructor of a class during object creation.
      - can only access static members of its class i.e. static variables and static methods.
      - The superclass constructor is not called automatically from the static initialization block.
      - called just once during the entire execution of the program when the class loads.
      - even called before the main method.
    - initializer blocks
      - An instance initialization block can be defined without using any special keyword.
      -  only executed when there is a call to the constructor during object creation.
      - can both static as well as non-static members of its class i.e. static and non-static variables and methods.
      - An automatic call to super class constructor is made by using the super() before executing any statement in the instance initialization block.
      - called as many times as a call to the constructor of the class is made.

## Static Inner class vs Inner class

- Nested classes class inside another class
- two types
  - static and non-static
  - Non-static nested classes are called inner classes.
- A nested class is a member of its enclosing class.
- Non-static nested classes (inner classes) have access to other members of the enclosing class, even if they are declared private
- Static nested classes do not have access to other members of the enclosing class.
- As a member of the OuterClass, a nested class can be declared private, public, protected, or package-private
  - outer classes can only be declared public or package-private
- Why Use Nested Classes?
  - It is a way of logically grouping classes that are only used in one place
  - It increases encapsulation
    - Only outer class can use it
  - It can lead to more readable and maintainable code
    - places the code closer to where it is used.
- a static nested class cannot refer directly to instance variables or methods defined in its enclosing class: it can use them only through an object reference.
- a static nested class is behaviorally a top-level class that has been nested in another top-level class for packaging convenience.
- an inner class is associated with an instance of its enclosing class and has direct access to that object’s methods and fields.
  - because an inner class is associated with an instance, it cannot define any static members itself.
- An instance of InnerClass can exist only within an instance of OuterClass and has direct access to the methods and fields of its enclosing instance.
- To instantiate an inner class, you must first instantiate the outer class. Then, create the inner object within the outer object
  - OuterClass.InnerClass innerObject = outerObject.new InnerClass();
- 	As main() method can’t be declared, regular inner class can’t be invoked directly from the command prompt.
- As main() method can be declared, the static nested class can be invoked directly from the command prompt.
