# Mutual Exclusion AKA Locks


- Anytime multiple threads are concurrently reading and writing a shared resource, it creates the potential for incorrect behavior, like a data race.
- But we can defend against that by identifying and protecting critical sections of code.
  - **A critical section or critical region is part of a program that accesses a shared resource, such as a data structure memory, or an external device, and it may not operate correctly, if multiple threads concurrently access it.**
  - The critical section needs to be protected so that it only allows one thread or process to execute in it at a time.
    -  The two threads experienced a data race as we added garlic to our shared shopping list, because incrementing a value is actually a three-step process. Read the current value, modify it, and then write back the result. Those three steps are critical section, and **they need to execute as an uninterrupted action, so we don't accidentally override each other.**
      -  Give me your pencil.  Now there's only one pencil for us to share, and the rule is that only the person holding the pencil can access the shopping list, either to read or write it. That way, one of us won't accidentally read a wrong value, because the other one is only halfway done updating it.
      - In this arrangement, the pencil is serving as a mechanism called a **mutex, short for mutual exclusion**, which you'll also hear referred to as a **lock**.
      - Only one thread or process can have possession of the lock at a time, so it can be used to prevent multiple threads from simultaneously accessing a shared resource, forcing them to take turns.
      - If either thread wants to access the shopping list, we first need to pick up the pencil, to acquire the lock on it. We do whatever we need to with the shared notepad, and then when we're done, release the lock by putting down the pencil.
      - The operation to acquire the lock is an **atomic operation, which means it's always executed as a single, indivisible action.** To the rest of the system, an atomic operation appears to happen instantaneously, even if under the hood, it really takes multiple steps.
        - The key here is that the atomic operation is an uninterruptible. - So, if a thread grab the pencil. Acquiring the mutex is an atomic action that no other thread can interfere with halfway through. Either you have the mutex, or you don't. And now that you do have a lock on our pencil, you can safely execute in the critical section.
        - Threads that try to acquire a lock that's currently possessed by another thread, can pause and wait till it's available.
        - Don't forget to release the mutex when you're done.
          -  Since threads can get blocked and stuck waiting for a thread in the critical section to finish executing, it's important to keep the section of code protected with the mutex as short as possible.
          - I should have returned the pencil as soon as I was done updating the list. That way another thread could use it to execute the critical section, while I'm busy doing other things.
