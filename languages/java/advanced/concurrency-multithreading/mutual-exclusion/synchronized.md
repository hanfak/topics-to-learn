# Synchronized

- To help create locks
- Used with method
  -  it automatically acquires the intrinsic lock for that method's object.
  -  That will prevent other threads that invoke a synchronized method on the same object from interleaving execution.
  - When a thread tries to invoke a synchronized method while another thread is executing a synchronized method for that same object, the second thread will suspend execution until the first thread is done and exits.
- Statements
  - When creating an synchronized statement, you specify the object that will provide the intrinsic lock.
  - Before a thread can execute the code contained within the synchronized statement, it must first acquire the intrinsic lock associated with the specified object and then when the thread is done, it will release its hold on that lock.

- https://dzone.com/articles/how-synchronization-works-in-java-part-1
- https://dzone.com/articles/how-synchronization-works-in-java-part-2
