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
    - https://www.java67.com/2019/09/how-to-write-generic-method-in-java.html
- Generic subtypes
  - https://dzone.com/articles/how-do-generic-subtypes-work
- Invariant
- generic types must be classes not primitives
- No generic arrays
  - `T[] arr = new T[10];// this code will not compile`
- Example ArrayList

- Bounded
    -
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

## rules
- Use the most generic types possible for arguments. Argument types provide the most utility when they are as generic as possible, because the method starts to apply to a wider range of input values.
- Use the most specific types possible for return values. Return types provide the most utility when they are as specific as possible, because a specific return value provides more functionality than a generic one.


## covariance and contravariance
- If type R derives from type T, and Foo<R> is a subtype of Foo<T>, Foo is covariant.
- If type R derives from type T, and Foo<T> is a subtype of Foo<R>, Foo is contravariant.
- If type R derives from type T, and Foo<R> is not related to Foo<T> in the type hierarchy, Foo is invariant.

If the Foo type has multiple type parameters, it can be covariant in regards to some of them, contravariant to some of them, and invariant to others still. For example, the Function interface in typical usage in Java is contravariant towards its first parameter but covariant towards its second parameter:

```java
Function<? super T, ? extends R>
```

This is as expected: a function that accepts any supertype of T can also handle T, and if we are able to handle its result type R, we will also be able to handle any of its subtypes.

### Links
- https://www.freecodecamp.org/news/understanding-java-generic-types-covariance-and-contravariance-88f4c19763d2/

## Raw types

- https://stackoverflow.com/questions/2770321/what-is-a-raw-type-and-why-shouldnt-we-use-it
- Allow for backwards compatiblity, before generics
- Only warning, as not compile time issue
  - but can lead to runtime issues
- Using Parameterized Types (generics) will prevent runtime issues by having a compiletime error

## Links

- https://enterprisecraftsmanship.com/posts/generic-types-arguments-specific-types-return-values/
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
- https://www.youtube.com/watch?v=K1iu1kXkVoA
- https://github.com/RichardWarburton/generics-examples/tree/master/src/main/java
- https://www.javacodegeeks.com/2019/04/variance-java.html
- https://www.java67.com/2019/07/top-50-java-generics-and-collection-interview-questions.html
