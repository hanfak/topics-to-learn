# Generics

- Boxing and Unboxing
- auto Boxing
- Casting
- Why?
  - https://howtodoinjava.com/java/generics/complete-java-generics-tutorial/
  - https://dzone.com/articles/hack-1-understanding-the-use-cases-of-generics
  - Move from runtime error to compile time error
  - Static safety
  - Avoid boiler plate code
  - More complex
- History
  - https://www.youtube.com/watch?v=LEAoMMEIUXk
- generic types
  - class
  - interface
  - methods
- Invariant
- generic types must be classes not primitives
- No generic arrays
  - `T[] arr = new T[10];// this code will not compile`
- Example ArrayList
- Bounded
  - extends
  - super
  - PECS
    - https://stackoverflow.com/questions/2723397/what-is-pecs-producer-extends-consumer-super
    - https://howtodoinjava.com/java/generics/java-generics-what-is-pecs-producer-extends-consumer-super/
    -
  - Multiple bounds
- Wild cards
  - https://stackoverflow.com/questions/18176594/when-to-use-generic-methods-and-when-to-use-wild-card
- No classic subtyping
  - compare `List<Number> numbers = new ArrayList<Integer>();` With `Number[] numbers = new Integer(10);`
- Flexible apis
- Type Erasure
  - compatibility with older java versions
- Intersection types
  - &
  - Binary compatiblity

## Links

- https://docs.oracle.com/javase/tutorial/java/generics/
- http://thegreyblog.blogspot.com/2011/03/java-generics-tutorial-part-i-basics.html
- https://www.javacodegeeks.com/2015/09/how-and-when-to-use-generics.html
- https://zeroturnaround.com/rebellabs/java-generics-cheat-sheet/
- https://dzone.com/articles/5-things-you-should-know-about-java-generics
- https://www.journaldev.com/1663/java-generics-example-method-class-interface
- http://www.java2novice.com/java-generics/
- http://www.angelikalanger.com/GenericsFAQ/JavaGenericsFAQ.html
- https://nofluffjuststuff.com/magazine/2016/09/time_to_really_learn_generics_a_java_8_perspective
- https://github.com/annimon-tutorials/Java-Generics-Tutorial/tree/master/src/test/java/com/example/generics
- https://www.youtube.com/watch?v=34oiEq9nD0M
- https://www.youtube.com/watch?v=9tHLV0u87G4
- https://github.com/RichardWarburton/generics-examples/tree/master/src/main/java
- https://www.javacodegeeks.com/2019/04/variance-java.html
- https://www.java67.com/2019/07/top-50-java-generics-and-collection-interview-questions.html