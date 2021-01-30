# Multithreading


- It allows multitasks to be executed simultaneously or in parallel to make the most of the computer hardware with multiple CPUs.
  - True parallel processing  happens when you have multi cores (or multi replica pods)
  - where as on a single core, multi threads must share the same cpu, and use switching mechanism to share the threads with the cpu (but generally so fast it seems in parallel)
- Increases performance and used to increase high throughput and lower latency
  - Poor performance is to allow a slow process being single threaded on a multi core cpu, as other cpu/resources are idle
  - In general, the maximum throughput is achieved when every processor is fully busy
  - If thread is waiting for something, then cpu is not busy
    - read/write to disk
    - network call
- Generally a tough area to design, to debug, and lots of possible bugs

## Drawbacks

- https://web.stanford.edu/~ouster/cgi-bin/papers/threads.pdf
- Difficulty of Writing Code
  - When you apply multithreading, you will push a lot of threads together at same time, on the same data, same objects, and same functions.
  - Need to control these and make them thread safe
    - **thread-safety occurs if all threads go inside the same function at the same time, and each thread can get exactly the data which they expected not the data of other thread.**
  - Causes of non thread safe code
    - static variables, static function, and singleton class etc
  - If all threads run at the same time, they will use the same static variables or function, and this thread will get the data of another thread.
  - Making threads safe
    - Synchronizing the critical sections
      - only 1 thread can work with this part at 1 time,
      - becareful as only for the source code which all thread can’t run together.
      - This will make the performance go down
    - Use immutable objects
    - Use thread-safe wrappers
      - put the main class (which isn’t thread-safe) inside a new class that is thread-safe
  - Ignore Deadlock
    - **The deadlock happens when one thread is waiting for the resource of other thread, but the other thread still waiting for the resource which keep by the first thread.**
    - To ignore the deadlock
      - Each thread has to process different data
      - Each thread have to create own object and function by themselves.
      - Don’t share the data between threads
  - Careful When Using Synchronized
    - will make the performance go down
    - only use it when you have to use
- Difficulty of Testing and Debugging
  - To deal with this
    - Keep the number of threads as a input parameter of main function if you can
      - we can set the number of threads to 1, and we have a single thread to test and debug
      - this way just supports finding the business bugs, and the bugs of single thread
      - If we got the problem with multiple threads like each threads have conflict with each other, this way is not helpful
    - Add useful log to the thread
      - try to put the log at the position which you can see the running flow, and you can see the whole flow
      - Write log when the exception happen,
    - Use the tool to test
      - jconsole
