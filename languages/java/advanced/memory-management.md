# Memory Management

- https://dzone.com/articles/java-memory-management
- http://tutorials.jenkov.com/java-concurrency/java-memory-model.html
- https://www.journaldev.com/4098/java-heap-space-vs-stack-memory
- http://www.baeldung.com/java-initialization

performance https://www.dynatrace.com/resources/ebooks/javabook/

## Debugging

- https://mydeveloperplanet.com/2018/11/14/how-to-solve-your-java-performance-problems-part-1/

## Heap and stack

- https://stackify.com/java-heap-vs-stack/
- https://www.journaldev.com/4098/java-heap-space-vs-stack-memory

### Defintions

- Shallow heap
  - is the memory consumed by one object. The actual memory consumed by one object depends on the underlying architecture.
- Retained Heap of an object
  - is the sum of shallow sizes of all objects in the retained set of that object.
- Retained set of an object
  - is the set of objects, which would be removed by GC when that particular object is garbage collected.
- A heap dump is a snapshot of the heap memory of a Java process at a given time.
  - The snapshot mainly consists of Java objects and classes.

## GArbage collection

- https://self-learning-java-tutorial.blogspot.co.uk/2014/07/garbage-collection.html
- https://stackify.com/what-is-java-garbage-collection/

## Memory leaks

- https://self-learning-java-tutorial.blogspot.co.uk/2014/07/what-is-memory-leak-in-java.html
- https://stackify.com/memory-leaks-java/
- https://www.baeldung.com/java-memory-leaks
- https://dzone.com/articles/how-memory-leaks-happen-in-java-apps
- https://www.toptal.com/java/hunting-memory-leaks-in-java
- https://www.dynatrace.com/news/blog/how-to-identify-a-java-memory-leak/


https://github.com/makersacademy/java_intro/blob/master/chapter0-What-is-Java/terminology.md

## Graphs

- saw tooth graph
  - https://stackoverflow.com/questions/47766884/why-does-heap-memory-usage-graph-look-like-this
- https://docs.azul.com/zing/UsingZing_GCLogAnalyser_HeapUseGraphs.htm

## Jmx

- https://stackify.com/asynchronous-programming-easier-think/
- https://self-learning-java-tutorial.blogspot.com/2018/07/jmx-tutorial.html

## Thread dumps

- https://self-learning-java-tutorial.blogspot.com/2018/08/working-with-jcmd-command.html
