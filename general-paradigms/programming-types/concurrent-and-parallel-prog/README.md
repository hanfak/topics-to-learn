# Concurrent and Parallel Programming

- threads
  - typically are spawned within a process without crossing the boundary of that process
  - ie multiple separate actions happening within the same jvm
    - Can be mimic wiht multiple replicas of jvms on server (ie replica pods on kubernetes cluster)
- processes
  - is a stand-alone program
  - ie A program running on a jvm
- Mutual exclusion
- locks

## Definitions

- Concurrency is about correctly and efficiently controlling access to shared resources
  - ie constructing thread safe data structures
  - primitives - locks, semaphores, coroutines
  - It is hard
    - reasoning about shared state and locks requires wizadary
- parallelism is about using additional resources to produce an answer faster
  - ie searching a large data set by partitioning
  - easeier
    - do it via partitioning
  - Just an optimisation only
    - only if it gets answer faster
    - just because we use more resources does not mean it is faster
      - need to think about splitting, doing the work, then combine the result
    - Need to measure performance (jconsole)
  - if additional resources are not avialable can still compute sequentially
  -

- https://www.freecodecamp.org/news/concurrency-parallelism-and-the-many-threads-of-santa-claus/
- https://completedeveloperpodcast.com/episode-152/
- http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html
