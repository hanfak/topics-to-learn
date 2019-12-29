# Semaphore

- A semaphore is another synchronization mechanism that can be used to control access to shared resources, sort of like a mutex, but unlike a mutex, a semaphore can allow multiple threads to access the resource at the same time, and it includes a counter to track how many times it's been acquired or released.
- As long as the semaphore's count value is positive, any thread can acquire the semaphore, which then decrements that counter value.
- If the counter reaches zero, then threads trying to acquire the semaphore will be blocked and placed in a queue to wait until it's available.
- When a thread is done using the resource, it releases the semaphore, which increments that counter value and if there are any other threads waiting to acquire the semaphore, they'll be signaled to wake up and do so.
- example
  - Hmm, looks like my phone's about to die. - Lucky us. There is a charger right here. - Nice, this charger has two ports. So it can be used by up to two devices at the same time. You can think of the number of open ports as a semaphore.
  - Right now, this semaphore has a value of two, because there are two free ports. And when T1 acquire one of these ports by plugging in it's phone, it decrements the semaphore's value to one. T2 will acquire the other port. And that decreases the semaphore's value to zero, which means it's unavailable for anyone else to use.
  - When T3 wants to use the charger, it cannot as the semaphore's locked right now because there aren't any available ports. T3 will have to wait until one of the threads is done charging and releases the semaphore.
  - Thus T3 will wait.
  - When a thread is done or exits for some condition, it can release  from the  port, which increments the semaphore's value and T1 will notify T3 that it's available.
    - now the semaphore's positive, T3 can acquire it and charge it's phone.
- This type of semaphore that we're using here is called a **counting semaphore**, because it can have a value of zero, one, two, three, and so on, to represent the number of resources we have.
- In our scenario, we're counting available charger ports but in software, a counting semaphore might be used to manage access among multiple threads to a limited pool of connections for something like a server or a database.
  - Or a counting semaphore could be used to track how many items are in a queue.
- Now, it's also common to restrict the possible values of a semaphore to only being either zero or one, with zero representing a locked state and one representing unlocked.
  - This is called a **binary semaphore**, and at first glance, it looks a lot like a mutex.
  - In fact, it can be used just like a mutex, with a thread acquiring and releasing the semaphore to lock and unlock it.
  - However, there is a key difference. **A mutex can only be unlocked by the same thread that originally locked it. A semaphore, on the other hand, can be acquired and released by different threads. Any thread can increment the semaphore's value by releasing it or attempt to decrement of value by acquiring it.**
    -  That may sound like a recipe for trouble and it certainly can be if you're not careful, but the ability for different threads to increment and decrement a semaphore's value and for threads to wait and be signaled by the semaphore is what **enables it to be used as a signaling mechanism**,
      - to synchronize the action between threads.
      - For example,
        - a pair of semaphores can be used in a similar way to condition variables to synchronize producer and consumer threads, adding and removing elements from a shared, finite queue or buffer. One semaphore tracks the number of items in the buffer, shown here as fillCount, and the other one tracks the number of free spaces, which I'll call emptyCount.
        - To add an element to the buffer, the producer will first acquire the emptyCount, which decrements its value, then it pushes the item into the buffer and finally it releases the fillCount semaphore to increment its value.
        - Now, on the other side of the buffer, when the consumer wants to take an item, it first acquires fillCount to decrement its value, then it removes an item from the buffer and finally increments the emptyCount by releasing it.
        - Notice that the producer and consumer each acquire a different semaphore as the first operation in their respective sequences. If the consumer tries to take an item when the buffer is empty, then when it tries to acquire that fillCount semaphore, it'll block and wait until a producer adds an item and releases fillCount, which will then signal the consumer to continue. Likewise, if the producer tries to add an item to the fillBuffer, then it goes to acquire the the emptyCount semaphore. It'll block and wait until a consumer removes an item and releases the emptyCount.