# Inheritance for reuse

- Breaks encapsulation and liskov subsitution
  - See example of Stack inheriting from Vector in Java
- Always refactor to use a wrapper pattern (adpater or decorator)

## How it works

- A subclass inherits from a class to inherit the behaviours that it can use in it's own new behaviour
```java
public class Stack<E> extends Vector<E> {

  public boolean empty() {
    return size() == 0;
  }

  public void push(E item) {
    add(item);
  }

  public E pop() {
    return remove(size()-1);
  }
}
```

## Issues

- Using an instance of the subclass, also has access to the methods of the super class
  - This can lead to the client using the subclass in ways it was not meant to be use, and possibly causing breaking behaviour
