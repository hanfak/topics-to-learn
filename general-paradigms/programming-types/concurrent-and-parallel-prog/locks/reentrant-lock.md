# Reentrant lock

- Only one person at a time can own or have a lock on it, and only that person can access a shared resource
  - If a thread attempt to lock the mutex while another thread has it, the thread will be blocked, and it will need to wait until he unlocks it so it becomes available.
  -  Well a thread can't unlock the mutex while its blocked waiting on it, and It will be waiting on the mutex forever because it will never be able to unlock it. It's stuck, and so are you.
  - **If a thread tries to lock a mutex that it's already locked, it'll enter into a waiting list for that mutex, which results in something called a deadlock**, because no other thread can unlock that mutex.
    - There may be times when a program needs to lock a mutex multiple times before unlocking it.
      - In that case, you should use a reentrant mutex to prevent this type of problem.
      - **A reentrant mutex is a particular type of mutex that can be locked multiple times by the same process or thread**. Internally, the reentrant mutex keeps track of how many times it's been locked by the owning thread, and it has to be unlocked an equal number of times before another thread can lock it.
      - If this pencil is a reentrant mutex, when I pick it up, I lock it. - Now someone's thread has a hold on the mutex, so it's the only one that can lock or unlock it. - Since the pencil is reentrant I can lock it again. Now the pencil has been locked twice by me, which means I'll have to unlock it twice to fully release my hold on it. **If your program needs to lock a mutex multiple times, using a reentrant mutex may seem like an easy way to avoid a deadlock**. But if you don't unlock the reentrant mutex the same number of times, you can still end up stuck. - I'm waiting. Thanks.
      - Many programmers like using reentrant locks because it can make things easier. You don't need to worry as much about what's already been locked, and they make it easier to retrofit locks into existing code.
      - As an example, say I have a function to increment a shared counter, and it uses a mutex to protect that operation. If later I create another function that uses the same mutex to protect some other section of code, and that section of code uses the increment counter function, since those functions are nested, when I execute my function it will end up locking the mutex twice before unlocking it. If I was using a regular non-reentrant lock, that would produce a deadlock, but with a reentrant mutex this works just fine.
  - Now like many things in the world of programmers, there are some very strong opinions about whether reentrant locks are good or evil.
    - Some opponents of using reentrant locks will say the code can be refactored to avoid having nested locks by using a third function that increments the counter and only gets called from within a protected section.
    - One use case where reentrant locks are really needed is when writing a recursive function, that is, a function that calls itself.
      - If the function makes a recursive call to itself from within a locked section, it will lock the mutex multiple times as it repeats itself, and then unlock the mutex an equal number of times as it returns and unwinds.
      -  Since a reentrant mutex can be used recursively like this, you'll often hear it referred to as a **recursive mutex or a recursive lock**.
