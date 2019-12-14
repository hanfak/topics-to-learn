# Threads

## Thread lifecycle

- threads can be in one of six possible states.
  - There's the usual new state for threads that have not yet been started,
  - the runnable state for threads that are executing in the Java virtual machine,
  - the blocked state which in Java means a thread is blocked waiting for a monitor lock
  - the terminated state for after a thread has exited.
  - The two additional states that Java adds are basically more specific variations of being blocked while waiting on other threads.
    - In the waiting state, a thread is waiting indefinitely for another thread to perform a particular action.
    - the timed waiting state, the thread will wait for another thread to perform an action for up to a specific waiting time.

## Thread attributes

- In addition to a threads state, which can be retrieved using the getState() method, there are a few other useful properties and methods for java threads
- If you need to access the thread that's currently executing, you can use the currentThread() method, which returns a reference to the currently executing thread object.
- Whenever a new thread gets created, it will be assigned a thread ID.
  - This is a positive long number that serves as a unique identifier for the thread, and remains unchanged during it's lifetime.
  - That thread ID can be retrieved using the getID() method.
  - Now, keep in mind that after a thread terminates, that ID number will be available for other new threads to reuse.
- Another related property is the threads name,
  - which is a string that can be used for identification purposes.
  - Now, more than one thread can have the same name, but they'll never have the same thread ID.
- There are several variations of the thread constructor method that allow you to specify the name when creating a thread, but if a name is not specified, then java will generate a new name for the thread, usually with a default format like Thread-N, where N is a positive integer.
-  Users can still change a threads name after creating it, by using the setName() method.
- And you can always retrieve it using the corresponding getName() method.
- Every thread also has a priority, which tells the java virtual machines thread scheduler when each thread should run relative to other threads.
  - And priority values range from one to 10, with one being the lowest priority, and 10 being the highest.
  - You can set and retrieve a threads priority using the setPriority() and getPriority() methods respectively.
- Now, one thing that java threads do not have is a way to directly identify their parent thread.
  - When a new thread is created, it's parent is used to set properties like the threads priority and it's daemon status.
  - But the child does not maintain a reference to it's parent thread.
  - One reason for that is that it enables the parent thread to be garbage collected by the jvm to reclaim memory, which would not be possible if the child thread was holding a reference to it.

## Creating threads

- Extend Thread class, and implement run() method
  - Cannot extend this class again
  - Each instance is a separate object
- Instantiate Thread class, and inject the a class that implements runnable
  - Multiple threads can share a single Runnable object, reduce memory usage
  - Recommended

## Testing for thread safety
  - https://dzone.com/articles/how-i-test-my-java-classes-for-thread-safety

## Links

- https://baptiste-wicht.com/posts/2010/05/java-concurrency-part-1-threads.html
