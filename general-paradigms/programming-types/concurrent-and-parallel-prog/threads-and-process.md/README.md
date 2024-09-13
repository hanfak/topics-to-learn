# Threads and processes

## When to use threads

scenarios where the task is either
1) IO blocking task 
- When you read from or write to disk, depending on how you do it and the kernel interface you used, the write might be blocking. This means the process that executes the IO will not be allowed to execute any more code until the write/read completes. 
- That is why you see most logging operations are done on a secondary thread (like libuv that Node uses) this way the thread is blocked but the main process/thread can resume its work. 
- If you can do file reads/writes asynchronously with say io_uring then you technically don't need threading. 
- Now notice how I said file IO because it is different than socket IO which is always done asynchronously with epoll/select etc.

2) CPU heavy
- The second use case is when the task requires lots of CPU time, which then starves/blocks the rest of the process from doing its normal job. So offloading that task to a thread so that it runs on a different core can allow the main process to continue running on its the original core.

3) Large volume of small tasks
- The third use case is when you have large amount of small tasks and single process can't deliver as much throughput. An example would be accepting connections, a single process can only accept connections so fast, to increase the throughput in case where you have massive amount of clients connecting, you would spin multiple threads to accept those connections and of course read and process requests. Perhaps you would also enable port reuse so that you avoid accept mutex locking.

### Not to use threads

- network I/O heavy workload, async I/O is far better than simple multi-threading.
  - Should use async, event looping, coroutines 