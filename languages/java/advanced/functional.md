# Functional Programming

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

## streams
  - map
  - filter
  - reduce
  - Other Reduce
    - count
    - distinct
    - sum
  - collect
    - Collectors.toList
  - infinite streams
    - https://dzone.com/articles/infinite-streams-in-java-8-and-9
  - lambdas that throw exceptions
    - https://medium.freecodecamp.org/why-you-should-ignore-exceptions-in-java-and-how-to-do-it-correctly-8e95e5775e58
  - https://flyingbytes.github.io/programming/java8/functional/part3/2017/02/18/Java8-Part3.html
  - Splitting streams 
    - https://flyingbytes.github.io/programming/java8/functional/part4/2017/03/10/Java8-Part4.html

## Collectors

- http://www.deadcoderising.com/2017-03-07-java-8-creating-a-custom-collector-for-your-stream/

## Method references

## lambdas/ Annoynmous functions

  - http://www.oracle.com/webfolder/technetwork/tutorials/obe/java/Lambda-QuickStart/index.html
  - https://dzone.com/articles/java-8-lambas-limitations-closures

## Functions

- https://flyingbytes.github.io/programming/java8/functional/part1/2017/01/23/Java8-Part1.html


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

  - https://docs.oracle.com/javase/8/docs/api/java/util/Optional.html
  - https://dzone.com/articles/java-optionals-for-more-expressive-code
  - https://flyingbytes.github.io/programming/java8/functional/part2/2017/02/04/Java8-Part2.html

## currying and partial functions

### Links

- https://www.linkedin.com/pulse/functional-programming-applying-currying-java-figueras/
- https://gist.github.com/timyates/7674005
- https://adorow.github.io/blog/2017/06/04/currying-in-java
- https://www.pgrs.net/2015/04/23/partial-function-application-in-java-8/
- https://medium.com/@andre_videla/excuse-me-sir-there-is-no-curry-in-my-java-2750284c7a1e

## Links

- https://www.sitepoint.com/java-8-streams-filter-map-reduce/
- https://zeroturnaround.com/rebellabs/java-8-explained-applying-lambdas-to-java-collections/
- https://docs.oracle.com/javase/8/docs/api/java/util/stream/package-summary.html
- http://www.devx.com/Java/functional-features-in-java-8.html
- https://github.com/winterbe/java8-tutorial
- https://dzone.com/articles/j%CE%BBv%CE%BB-8-a-comprehensive-look
