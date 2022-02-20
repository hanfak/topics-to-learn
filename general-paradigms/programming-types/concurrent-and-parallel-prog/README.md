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

###  Multithreading
- you have multiple threads of execution inside the same application.
- a multithreaded application is like an application that has multiple CPUs executing different parts of the code at the same time.
- There are similarities with multitasking and distributed systems
- Also known as concurrency

#### Why
- Better utilization of a single CPU.
  - to be able to better utilize the resources in the computer
  - ie  if one thread is waiting for the response to a request sent over the network, then another thread could use the CPU in the meantime to do something else.
  - if the computer has multiple CPUs, or if the CPU has multiple execution cores, then multithreading can also help your application utilize these extra CPU cores.
- Better utilization of multiple CPUs or CPU cores.
  - you need to use multiple threads for your application to be able to utilize all of the CPUs or CPU cores.
  - A single thread can at most utilize a single CPU
    - Some cases not all the cpu (ie waiting for network call)
- Better user experience with regards to responsiveness.
  - Example: if you click on a button in a GUI and this results in a request being sent over the network, then it matters which thread performs this request. If you use the same thread that is also updating the GUI, then the user might experience the GUI "hanging" while the GUI thread is waiting for the response for the request. Instead, such a request could be performed by a backgroun thread so the GUI thread is free to respond to other user requests in the meantime.
  - Example: a server application that listens on some port for incoming requests. when a request is received, it handles the request and then goes back to listening. If the request takes a long time to process, no new clients can send requests to the server for that duration. Only while the server is listening can requests be received
    - An alternate design would be for the listening thread to pass the request to a worker thread, and return to listening immediatedly. The worker thread will process the request and send a reply to the client. the server thread will be back at listening sooner. Thus more clients can send requests to the server.
- Better user experience with regards to fairness.
  -  to share resources of a computer more fairly among users.
  - example:  a server that receives requests from clients, and only has one thread to execute these requests. If a client sends a requests that takes a long time to process, then all other client's requests would have to wait until that one request has finished. By having each client's request executed by its own thread then no single task can monopolize the CPU completely.
- Simple design
  - Example
    -  If you were to program the ordering of reading and processing by hand in a singlethreaded application, you would have to keep track of both the read and processing state of each file.
    - Instead you can start two threads that each just reads and processes a single file. Each of these threads will be blocked while waiting for the disk to read its file.
    - While waiting, other threads can use the CPU to process the parts of the file they have already read.
    - The result is, that the disk is kept busy at all times, reading from various files into memory. This results in a better utilization of both the disk and the CPU. It is also easier to program, since each thread only has to keep track of a single file.

#### Issues

- Complex design
  - Code executed by multiple threads accessing shared data need special attention. Thread interaction is far from always simple.
  - Errors arising from incorrect thread synchronization can be very hard to detect, reproduce and fix.
- Context Switching Overhead
  - When a CPU switches from executing one thread to executing another, the CPU needs to save the local data, program pointer etc. of the current thread, and load the local data, program pointer etc. of the next thread to execute. This switch is called a "context switch". The CPU switches from executing in the context of one thread to executing in the context of another.
  - Context switching isn't cheap. You don't want to switch between threads more than necessary.
- Increased Resource Consumption
  - A thread needs some resources from the computer in order to run. Besides CPU time a thread needs some memory to keep its local stack. It may also take up some resources inside the operating system needed to manage the thread.
  - Try creating a program that creates 100 threads that does nothing but wait, and see how much memory the application takes when running.
#### Is hard

- The threads are executing within the same program and are hence reading and writing the same memory simultaneously.
- example
  - If a thread reads a memory location while another thread writes to it,
    - what value will the first thread end up reading?
    - The old value?
    - The value written by the second thread?
    - Or a value that is a mix between the two?
  - if two threads are writing to the same memory location simultaneously,
    - what value will be left when they are done?
    - The value written by the first thread?
    - The value written by the second thread?
    - Or a mix of the two values written?
- Without proper precautions any of these outcomes are possible. The behaviour would not even be predictable. The outcome could change from time to time.
  - Precautions meaning learning to control how threads access shared resources like memory, files, databases etc.

### Multithreading vs Multitasking
-  multitasking on single cpu computers
  - computers could execute multiple programs (AKA tasks or processes) at the same time. It wasn't really "at the same time" though. The single CPU was shared between the programs. The operating system would switch between the programs running, executing each of them for a little while before switching.
  -  Programs can no longer assume to have all the CPU time available, nor all memory or any other computer resources. A "good citizen" program should release all resources it is no longer using, so other programs can use them.
- Later came multithreading
  -  you could have multiple threads of execution inside the same program


### threads
-  like a separate CPU executing your application
  - A thread is not equal to a CPU though. Usually a single CPU will share its execution time among multiple threads, switching between executing each of the threads for a given amount of time.
  - It is also possible to have the threads of an application be executed by different CPUs.
- typically are spawned within a process without crossing the boundary of that process
- ie multiple separate actions happening within the same jvm
  - Can be mimic wiht multiple replicas of jvms on server (ie replica pods on kubernetes cluster)
### Concurrency is about correctly and efficiently controlling access to shared resources
- ie constructing thread safe data structures
- primitives - locks, semaphores, coroutines
- It is hard
  - reasoning about shared state and locks requires wizadary
### parallelism
- is about using additional resources to produce an answer faster
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
