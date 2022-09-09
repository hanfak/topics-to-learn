# Memory Management

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Memory Management](#memory-management)
	- [Debugging](#debugging)
	- [Heap and stack](#heap-and-stack)
		- [Defintions](#defintions)
	- [GArbage collection](#garbage-collection)
	- [Memory leaks](#memory-leaks)
	- [Heap dumps](#heap-dumps)
	- [Graphs](#graphs)
	- [Jmx](#jmx)
	- [Thread dumps](#thread-dumps)
	- [Jstat](#jstat)
	- [Benchmarking](#benchmarking)

<!-- /TOC -->

- https://dzone.com/articles/java-memory-management
- http://tutorials.jenkov.com/java-concurrency/java-memory-model.html
- https://www.journaldev.com/4098/java-heap-space-vs-stack-memory
- http://www.baeldung.com/java-initialization
- https://examples.javacodegeeks.com/java-memory-management/
- https://youtu.be/LCSqZyjBwWA The Java Memory Model - The Basics
- https://youtu.be/bspS-uTK0IM Understanding JVM Memory, Heap, Garbage Collection and Monitoring the JVM | Tech Primers
- https://www.youtube.com/watch?v=JLFjY6Ixct8 A Visual Introduction to Inner-Workings of the JVM - Douglas Hawkins
- https://opensource.com/article/22/4/jvm-parameters-java-developers

performance https://www.dynatrace.com/resources/ebooks/javabook/

## Debugging

- https://mydeveloperplanet.com/2018/11/14/how-to-solve-your-java-performance-problems-part-1/

## Heap and stack

- https://stackify.com/java-heap-vs-stack/
- https://www.journaldev.com/4098/java-heap-space-vs-stack-memory
- https://dzone.com/articles/stack-vs-heap-understanding-java-memory-allocation
- https://gribblelab.org/CBootCamp/7_Memory_Stack_vs_Heap.html


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
- https://roytuts.com/what-is-the-purpose-of-garbage-collection-in-java/

## Memory leaks

- https://self-learning-java-tutorial.blogspot.co.uk/2014/07/what-is-memory-leak-in-java.html
- https://stackify.com/memory-leaks-java/
- https://www.baeldung.com/java-memory-leaks
- https://dzone.com/articles/how-memory-leaks-happen-in-java-apps
- https://www.toptal.com/java/hunting-memory-leaks-in-java
- https://www.dynatrace.com/news/blog/how-to-identify-a-java-memory-leak/
- https://dzone.com/articles/what-to-do-about-java-memory-leaks-tools-fixes-and
- https://dzone.com/articles/how-to-find-and-fix-memory-leaks-in-your-java-appl


https://github.com/makersacademy/java_intro/blob/master/chapter0-What-is-Java/terminology.md


## Heap dumps

- https://www.javacodegeeks.com/2019/10/7-options-to-capture-java-heap-dumps.html


## Graphs

- saw tooth graph
  - https://stackoverflow.com/questions/47766884/why-does-heap-memory-usage-graph-look-like-this
- https://docs.azul.com/zing/UsingZing_GCLogAnalyser_HeapUseGraphs.htm

## Jmx

- https://stackify.com/asynchronous-programming-easier-think/
- https://self-learning-java-tutorial.blogspot.com/2018/07/jmx-tutorial.html

## Thread dumps

- https://self-learning-java-tutorial.blogspot.com/2018/08/working-with-jcmd-command.html

## Jstat

- https://www.javacodegeeks.com/2019/11/jstat-analysis.html

## Benchmarking

- Use Benchmarking to find out current performance
	- used to decide where to optimise
- Benchmarking and microbenchmarking on the JVM is hard
	- need to consider the following:
		- warm-up
		- HotSpot compilation
		- code optimizations like inlining and dead code elimination
		- multithreading
		- consistency of measurement
		- and more
- Tooling
	- https://github.com/openjdk/jmh
- JVM visualisation tools
