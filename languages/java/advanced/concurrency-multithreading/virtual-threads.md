# Virtual Threads

A new feature in java 19+

https://openjdk.java.net/jeps/425
- https://cr.openjdk.java.net/~rpressler/loom/Loom-Proposal.html
- https://itnext.io/kotlin-coroutines-vs-java-virtual-threads-a-good-story-but-just-that-91038c7d21eb


## structured concurrency 

- use of java 21 running of conncurrency in a structured/procedural way, instead of using completable future (callback) 
- Makes following the code easier to read
- Observable, the stack trace points to correct location of failure
- exception handling is more intuitive 
- Error handling short circuiting
  - if one fails then other sub tasks will fail if need all tasks to complete

### Links 
- https://www.youtube.com/watch?v=fbI3qveS_Is
  - Structured Concurrency in Java: The What & Why • Balkrishna Rawool • GOTO 2023
  - https://github.com/balkrishnarawool/StructuredConcurrency
- https://www.happycoders.eu/java/structured-concurrency-structuredtaskscope/
- https://quarkus.io/blog/virtual-thread-1/