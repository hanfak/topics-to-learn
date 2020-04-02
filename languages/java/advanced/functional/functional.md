# Functional Programming

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Functional Programming](#functional-programming)
	- [ISsues](#issues)
		- [To use FP in java correctly](#to-use-fp-in-java-correctly)
	- [Immutability](#immutability)
		- [Links](#links)
	- [streams](#streams)
		- [Checked exceptions](#checked-exceptions)
		- [Map and FlatMap](#map-and-flatmap)
	- [Collectors](#collectors)
	- [Method references](#method-references)
	- [lambdas/ Annoynmous functions](#lambdas-annoynmous-functions)
	- [Functions](#functions)
	- [Functional interfaces](#functional-interfaces)
		- [Links](#links)
	- [Moving from imperative to functional style](#moving-from-imperative-to-functional-style)
	- [Optional](#optional)
		- [Links](#links)
	- [Comparators](#comparators)
	- [currying and partial functions](#currying-and-partial-functions)
		- [Links](#links)
	- [Parallel an async](#parallel-an-async)
	- [Links](#links)

<!-- /TOC -->

- https://www.javacodegeeks.com/2017/09/overview-functional-programming.html
- https://tedvinke.wordpress.com/2017/11/07/functional-java-by-example-part-1-from-imperative-to-declarative/

## ISsues

- Just because you are using Lambda expressions, does not mean you are doing functional programming.
  - Lambda expressions in Java are simply a less verbose way of creating (slightly constrained) Objects and as such the most likely outcome of adopting Lambda’s without a good understanding of core functional concepts is gnarly, twisted, hard to follow, obfuscated imperative Object Oriented code with a nice concise syntax.
- Java is not a functional language, it is fundamentally an Object Oriented language that allows us to adopt some functional concepts in so far as we enforce their correct implementation through developer discipline

### To use FP in java correctly

- Make good use of Generic Types
  - Don’t ignore type parameters, declare them and enforce them everywhere.
  - Minimize casting and if instanceOfing
    - Where you do use them centralize each type of cast within a resuable method,
  - use proper type parameters on the inputs and outputs
  -  write good tests!
- Make illegal states unrepresentable in our code.
  - Avoid nulls,
    - Optionals
      - Use sparingly and not for fields (apart from data objects)
    - Dont allow null fields
    - USe inheritance
  - don’t throw Exceptions,
  - avoid locking and synchronization
- Make our own data classes immutable and final where possible,
  - use immutable collections (proper ones).
  - Avoid instanceof checks where possible, and
  - where you use them make sure the types are not extensible.
- Mse libraries that avoid runtime magic and reflection where pragmatically possible.

## Immutability

- Declare the class as final so it can’t be extended.
  - make the constructor private and construct instances in factory methods.
- Make all fields private so that direct access is not allowed.
- Don’t provide setter methods for variables
- Make all mutable fields final so that it’s value can be assigned only once.
- Initialize all the fields via a constructor performing deep copy.
- Perform cloning of objects in the getter methods to return a copy rather than returning the actual object reference.
- If the instance fields include references to mutable objects, don't allow those objects to be changed:
  -Don't provide methods that modify the mutable objects.
  - Don't share references to the mutable objects.
  - Never store references to external, mutable objects passed to the constructor;
    - if necessary, create copies, and store references to the copies.
    - Similarly, create copies of your internal mutable objects when necessary to avoid returning the originals in your methods.


### Links
- https://stackoverflow.com/questions/50257305/java-making-a-class-immutable
- https://www.journaldev.com/129/how-to-create-immutable-class-in-java
- https://medium.com/@mykola.shumyn/immutable-classes-in-java-76635df0356d
- https://dzone.com/articles/taming-concurrency-with-immutability
- https://reflectoring.io/java-immutables/
-

## streams

	- Streams
		- Give lazy evaluation (ie filter)
			- Also gives visual reminder that lazy evaluation is happening
			- Lazy evaluation will only happen when the terminal operation is hit ie forEach
		- Act like an iterator
  - filter
		- lazy
  - reduce
		- terminal op
		- converts a stream into something concrete
			- takes a collection and reduces to a single value
			- Take a collection and reduce to another collection
		- Other Reduce
	    - count
	    - distinct
	    - sum
	- map
	- forEach
		- terminal op
  - collect
		- Is a reduce operator
    - Collectors.toList
  - infinite streams
    - https://dzone.com/articles/infinite-streams-in-java-8-and-9
  - lambdas that throw exceptions
    - https://medium.freecodecamp.org/why-you-should-ignore-exceptions-in-java-and-how-to-do-it-correctly-8e95e5775e58
  - https://flyingbytes.github.io/programming/java8/functional/part3/2017/02/18/Java8-Part3.html
  - Splitting streams
    - https://flyingbytes.github.io/programming/java8/functional/part4/2017/03/10/Java8-Part4.html


### Checked exceptions

- need to add try catch in the stream, not great

```java
list.stream()
    .map(i -> i.toString())
    .map(s -> s.toUpperCase())
    .forEach(s -> System.out.println(s));
```

If they throw checked exceptions

```java
list.stream()
    .map(i - > {
        try {
            return i.toString();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    })
    .map(s - > {
        try {
            return s.toUpperCase();
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    })
    .forEach(s - > {
        try {
            System.out.println(s);
        } catch (Exception e) {
            throw new RuntimeException(e);
        }
    });
```


### Map and FlatMap

- FlatMap
  - thinks of it as MapFlatter, it maps (applies a function) then flattens it
  - https://www.mkyong.com/java8/java-8-flatmap-example/
- https://www.baeldung.com/java-difference-map-and-flatmap
- https://stackoverflow.com/questions/26684562/whats-the-difference-between-map-and-flatmap-methods-in-java-8

## Collectors

- http://www.deadcoderising.com/2017-03-07-java-8-creating-a-custom-collector-for-your-stream/

## Method references

## lambdas/ Annoynmous functions

  - http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/Lambda-QuickStart/index.html
  - https://dzone.com/articles/java-8-lambas-limitations-closures

## Functions

- https://flyingbytes.github.io/programming/java8/functional/part1/2017/01/23/Java8-Part1.html
- https://dzone.com/articles/functional-programming-functions


## Functional interfaces
  - supplier
  - consumer
  - function
  - predicate
  - unary operator
  - binary operator


### Links

- https://www.javacodegeeks.com/2018/01/functional-interface-java-8-functional-annotation-examples.html
- https://github.com/winterbe/java8-tutorial

  - https://docs.oracle.com/javase/8/docs/api/java/util/function/package-summary.html

## Moving from imperative to functional style

## Optional
  - of
  - isPresent
  - using map

### Links
  - https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html
  - https://dzone.com/articles/java-optionals-for-more-expressive-code
  - https://flyingbytes.github.io/programming/java8/functional/part2/2017/02/04/Java8-Part2.html

## Comparators

- https://examples.javacodegeeks.com/core-java/java-8-comparator-example/

## currying and partial functions

### Links

- https://www.linkedin.com/pulse/functional-programming-applying-currying-java-figueras/
- https://gist.github.com/timyates/7674005
- https://adorow.github.io/blog/2017/06/04/currying-in-java
- https://www.pgrs.net/2015/04/23/partial-function-application-in-java-8/
- https://medium.com/@andre_videla/excuse-me-sir-there-is-no-curry-in-my-java-2750284c7a1e

## Parallel an async

- https://www.javacodegeeks.com/2018/04/parallel-and-asynchronous-programming-in-java-8.html

## Links

- https://www.sitepoint.com/java-8-streams-filter-map-reduce/
- https://zeroturnaround.com/rebellabs/java-8-explained-applying-lambdas-to-java-collections/
- https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html
- http://www.devx.com/Java/functional-features-in-java-8.html
- https://github.com/winterbe/java8-tutorial
- https://dzone.com/articles/j%CE%BBv%CE%BB-8-a-comprehensive-look
