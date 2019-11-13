# Debugging Performance

## Getting Heap dump

- A heap dump is a snapshot of the heap memory of a Java process at a given time.
  - The snapshot mainly consists of Java objects and classes.
- For capturing  `java.lang.OutOfMemoryError`
  - java.lang.OutOfMemoryError
    - occur when the application tries to add more objects into the heap and there is no space left.
    - This will happen when the maximum heap size set in the start of the application is filled with objects
    - the garbage collector is not able to free up the memory because the all objects in heap still have some references
    - Causes
      - The application may need more memory to run; the currently allocated heap size is not enough to accommodate the objects generated during the runtime.
      - Due to a coding error in the application which is keeping the references of unwanted objects.
- Should capture heap dump right at that point to diagnose the problem because you want to know what objects were sitting in memory and what percentage of memory they were occupying when java.lang.OutOfMemoryError occurred.
  - Often, the app is restarted and the heap dump is not captured to analyse
- `XX:+HeapDumpOnOutOfMemoryError` as part of the java options
  - will capture heapdumps when java.lang.OutOfMemoryError occurs
  - `-XX:HeapDumpPath=/opt/tmp/heapdump.bin` to specify location of heapdump
  - By default, the heap dump is created in a file called `java_pid pid .hprof` in the working directory of the VM
- To record a dump, first run `jps` to find the process's PID, then run `jmap -dump:live,format=b,file=(dumpfile) (pid)`
  - If you get the error "Unable to open socket file: target process not responding or HotSpot VM not loaded", it probably means the process is running as a different user.
    - Add sudo -u (process user) in front of the command line, or run jmap as root with the -F flag.

## Analysing Heap dumps

- use of tools
  - JVisualVM (comes with jdk)
  - Eclipse Memory Analyzer (prefered)
    - https://www.eclipse.org/mat/
  - Jhat
  - https://visualvm.github.io/
  - https://www.jclarity.com/products/
  - Programmatically
    - https://blogs.oracle.com/sundararajan/programmatically-dumping-heap-from-java-applications
- Process
  - https://dzone.com/articles/java-heap-dump-analyzer-1
  - https://medium.com/@chrishantha/basic-concepts-of-java-heap-dump-analysis-with-mat-e3615fd79eb
  - https://www.evanjones.ca/java_memory_leaks.html
  - https://dzone.com/articles/finding-java-memory-leaks-from-a-heap-dump
  - https://www.youtube.com/watch?v=JoQN4xoXY5Y
  - https://www.youtube.com/watch?v=_gineh_HcoQ
  - https://www.youtube.com/watch?v=E2KYTXKUsT4
  - https://www.youtube.com/watch?v=iixQAYnBnJw
- In object list
  - This groups objects by class, ordered them from most to least number of instances. If you have a long running leak, it is probably one of the classes near the top of this list.
  -  need to look for "suspicious" classes: those that have "too many" instances, or are occupying too much memory.

## Dealing with out of memory errors

- Can set the java options `-Xmx<size>` and `-Xms<size>`
- Can retune the garbage collection
  - For example:
    - `-XX:-UseParallelGC`
      - Use parallel garbage collection for scavenges.
    - `-XX:-UseParallelOldGC`
      - Use parallel garbage collection for the full collections. Enabling this option automatically sets -XX:+UseParallelGC.
    - `-XX:NewRatio`
      - Ratio of old/new generation sizes. The default value is 2.
    - `-XX:SurvivorRatio`
      - Ratio of eden/survivor space size. The default value is 8.
    - `-XX:ParallelGCThreads`
      - Sets the number of threads used during parallel phases of the garbage collectors. The default value varies with the platform on which the JVM is runnin
  - Relationship between GC and Heap size
    - Larger Heap size will increase the GC execution time, but decrease the number of GC executions.
    - Smaller Heap Size will increase the number of GC executions, but decrease the GC execution time
- Analyse code flow and heap dump to find unwanted objects on the heapdump

## Preventative measures

- https://stackify.com/java-memory-leaks-solutions/
