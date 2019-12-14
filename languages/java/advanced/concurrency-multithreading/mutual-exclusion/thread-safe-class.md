# Thread safe class

- No State
  - avoiding instance or static variables.
  - Methods in classes without instance variables do only use local variables and method arguments.
- No Shared State
  - If you cannot avoid state, do not share the state. The state should only be owned by a single thread.
  - You can achieve thread-local instance variables by extending the thread class and adding an instance variable
  ```java
  package java.util.concurrent;
  public class ForkJoinWorkerThread extends Thread {
      final ForkJoinPool pool;
      final ForkJoinPool.WorkQueue workQueue;
  }
  ```
  - The other way to achieve thread-local variables is to use the class java.lang.ThreadLocal for the fields you want to make thread-local.
  ```Java
  public class CallbackState {
    public static final ThreadLocal<CallbackStatePerThread> callbackStatePerThread = new ThreadLocal<CallbackStatePerThread>() {
          @Override
          protected CallbackStatePerThread  initialValue() {
           return getOrCreateCallbackStatePerThread();
          }
       };
  }

  // To use

  CallbackStatePerThread callbackStatePerThread = CallbackState.callbackStatePerThread.get();
  ```
- Message Passing
  - If you do not share state using the above techniques, you need a way for the threads to communicate. A technique to do this is by passing messages between threads.
  - You can implement message passing using a concurrent queue
  - use a framework like Akka, a framework for actor style concurrenc
- Immutable State
  - To avoid the problem where a sending thread changes the message when the message is read by another thread, messages should be immutable.
  - you should declare its fields as final. This not only makes sure that the compiler can check that the fields are in fact immutable but also makes them correctly initialized even when they are incorrectly published.
- Use the Data Structures From java.util.concurrent
- Synchronized Blocks
  - If you cannot use one of the above techniques, use this
  - By putting a lock inside a synchronized block, you make sure that only one thread at a time can execute this section.
  - when you use multiple nested synchronize blocks, you risk deadlocks.
- Volatile Fields
  - Normal, nonvolatile fields can be cached in registers or caches. Through the declaration of a variable as volatile, you tell the JVM and the compiler to always return the latest written value
  - You can use volatile fields if the writes do not depend on the current value. Or if you can make sure that only one thread at a time can update the field.
- Atomic updates:
  - A technique in which you call atomic instructions like compare and set provided by the CPU
- java.util.concurrent.locks.ReentrantLock:
  - A lock implementation that provides more flexibility than synchronized blocks
- java.util.concurrent.locks.ReentrantReadWriteLock: A lock implementation in which reads do not block reads
- java.util.concurrent.locks.StampedLock
  - a nonreeantrant Read-Write lock with the possibility of optimistically reading values.
