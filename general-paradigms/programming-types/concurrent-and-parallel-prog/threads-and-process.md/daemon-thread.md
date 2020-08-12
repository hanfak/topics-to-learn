# Daemon Thread

- We often create threads to provide some sort of service, or perform a periodic task in support of the main program.
  - A common example of that is garbage collection.
  - A garbage collector is a form of automatic memory management that runs in the background and attempts to reclaim garbage, or memory that's no longer being used by the program.
  - Many languages include garbage collection as a standard part of their run time environment, but for this demonstration, I'll spawn my own new thread to handle garbage collection.
    - The GC thread is a separate child thread that will execute independently of my main thread.
    - So, I can continue doing what I'm doing here, getting my soup ingredients ready.
    -  While GC thread try to reclaim some memory, or counter space, by clearing out main thread's garbage.
    - This set-up, with GC thread running as a separate thread to provide that garbage collection service, will work fine until I'm ready to finish executing.
    - Bam, now my soup's spiced and ready, my main thread is done executing, and I'm ready to exit the program.
    - But I can't. - Because GC thread still running. Since maint thread spawned me as a normal child thread, it won't be able to exit until I've terminated.
    - - And since GC thread's is designed to collect garbage in a continuous loop, it'll never exit. I'll be stuck here waiting forever, and this process will never terminate.
  - Threads that are performing background tasks, like garbage collection, can be detached from the main program by making them what's called a daemon thread.
  - **A daemon thread, which you may also hear pronounced as Damon, is a thread that will not prevent the program from exiting if it's still running.**
  -  By default, **new threads are usually spawned as non-daemon or normal threads, and you have to explicitly turn a thread into a daemon or background thread.** O
  - When my main thread is finished executing and there aren't any non-daemon threads left running, this process can terminate.
    - And GC thread's daemon thread will terminate with it.
    - Since GC thread was terminated abruptly with the process, I didn't have a chance to gracefully shut down and stop what I was doing.
      - That's fine in the case of a garbage collection routine, because all of the memory this process was using will get cleared as part of terminating it.
      - But if I was doing some sort of IO operation, like writing to a file, then terminating in the middle of that operation could end up corrupting data.
    - **If you detach a thread to make it a background task, make sure it won't have any negative side-effects if it prematurely exits.**