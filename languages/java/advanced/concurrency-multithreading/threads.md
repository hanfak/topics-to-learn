# Threads

- Avoid dealing with these manually, use executor library or other concurency libraries (actors etc)
- Developers do not need to think in terms of the stack (let the compiler and runtime system deal with it) or the heap (let GC deal with it)
  - Developers should do the same with threads, and not handle them manually
  - Threads should be considered a managed resource like heap and stack
-  Developers use concurrency and parallelism which is founded on the theory of constructing operating systems (From the 60s)
  -  There have been improvements
-  Going into too much details ie using synchronized statements, locks, mutexes, this is too detailed (For most things)
-  **Instead of creating threads explicitly and managing them, construct tasks and submit them to a thread pool**
-  **If you have many tasks that need to communicate with one another, then rather than using shared memory, use a thread-safe queue instead.**
- For example,
  - Golang programming language. It is all about sequential processes communicating, made to execute via an underlying thread pool.
- Many use the terms actors, dataflow, CSP, or active objects are variations of sequential processes communicating
  - Fork/Join framework, which can be used explicitly and also underpins the Streams library
  - other librarieslike Akka, Qusar
