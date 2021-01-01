# CountDownLatch


## Uses

- launch multiple concurrent tasks, and then wait on their completion before proceeding further.
- Can use Executor service
```java
ExecutorService pool = Executors.newFixedThreadPool(5);
Future<?> future = pool.submit(() -> {
  // Your task here
});
```
- Use of CountDownLatch helps us wait for all of tasks to complete
-  testing your concurrent code, since it allows you to make sure that all the tasks are complete before checking their results
- ie
  - You have a proxy and an embedded server, and you’d like to test that when the proxy is called, it invokes the correct endpoint on your server.
  - it doesn’t make much sense to issue a request before both the proxy and server have started. One solution is to pass a CountDownLatch to both methods, and continue with the test only when both parties are ready
  
## How it works

- A CountDownLatch takes the number of invocations as a constructor argument.
- Each task then holds a reference to it, calling the countDown method when the task completes
- For example, will launch 16 tasks, then wait for them to finish before proceeding further.
```java
int tasks = 16;
CountDownLatch latch = new CountDownLatch(tasks);
for (int i = 0; i < tasks; i++) {
  Future<?> future = pool.submit(() -> {
    try {
      // Your task here
    } finally {
      latch.countDown();
    }
  });
}
if (!latch.await(2, TimeUnit.SECONDS)) {
  // Handle timeout
}

```
- Factors to know about when using
  - Make sure that you release the latch in a finally block. Otherwise, if an exception occurs, your main thread may wait forever.
  - Use the await method that accepts a timeout period. That way, even if you forget about the first point, your thread will wake up sooner or later.
  - Check the return value of the method. It returns false if the time has elapsed, or true if all the tasks managed to complete on time.

## Beware

- you shouldn’t use it in production code that makes use of concurrent
libraries or frameworks
  - ie kotlin coroutines
- Why
  - Different concurrency models don’t play well together.
