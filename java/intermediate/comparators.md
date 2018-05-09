# Comparators

## Comparable interface

- One method to implement, `compareTo`
  - Takes another other object of same class that implements it and returns an `int`
  - signature: `public int compareTo(T o);`
- Why Use
  - The objects created from the class has a natural ordering
  - allows classes like collections to use it when doing sort for example.
  - use for any class with alphanumeric or chronological ordering
- Rules
  - return 0 if both objects are equal
  - return less than one, when the current object is less than the object passed into the compareTo method
  - return greater than one, when the current object is more than the object passed into the compareTo method
- Using a comparator in compareTo
  - See github link????
- Use comparator constructor method
  - can use like a builder, and chain multiple compares and in the order you want them to compare to.
  - see github??
- Using a field's object compareTo method in the current object
  - exmaple:

  ```java
  public class Duck implements Comparable<Duck> {
    public String name;

    public Duck(String name) {
        this.name = name;
      }

    public int compareTo(Duck d) {
      return name.compareTo(d.name);
    }
  }
  ```
    - Using the field name of duck objects to compare with each other.
    - name is a String Type, and String implements Comparable. thus can use compareTo from String
  - Another Example
    - see github ???
  - Note all classes/types will have an implementation of comparable, so will not be able to call it's compareTo method

- Using own method
  - Example

  ```java
  public class Duck implements Comparable<Duck> {
    public int age;

    public Duck(int age) {
        this.age = age;
      }

    public int compareTo(Duck d) {
      return age - d.age;
    }
  }
  ```
    - comparing on the age of duck, but it's field is a primitive and does not have a compareTo method
      - could create an integer wrapper class and compareTo on that, as Integer implements compareTo
  - see github ???
  - Avoid this way of doing it
    - arithemtic overflow issues
- Use of > and < and ==
  - Avoid as verbose and error prone
  - see github???
- Comparing multiple fields
  - see githubg???
- Static compare method
  - see github???
- Comparable and equals
  - make them consistent
  - override equals() and set it to true when comparable has two objects equal returns 0
  - If not possible, write a comment saying this inconsistent
- Good practices
  -

### Links

- https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html

## Comparators

- reversed
  - instead of Comparator<ComparableItem4> COMPARATOR = (x1,x2) -> x2.price - x1.price; to ????
- lambda
  - Comparator<Duck> c = (d1, d2) -> d1.age - d2.age;
  - refactor to use comparator constructor method
    - Comparator<ComparableItem4> COMPARATOR = (x1,x2) -> x1.price - x2.price; to Comparator.comparingInt(x -> x.price);
- Old way
  - Example >???
- Chainging comparing
  - http://www.baeldung.com/java-8-comparator-comparing
- passing into sorted() and sort()

### Links

- https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html
- https://www.javabrahman.com/java-8/the-complete-java-8-comparator-tutorial-with-examples/

### Collection.sort or stream.sorted()

## Links

- http://www.baeldung.com/java-comparator-comparable
