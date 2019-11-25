# Starvation

- It would be nice if Olivia and I took turns acquiring and releasing the pair of chopsticks so we could each take an equal amount of sushi from the shared plate. But that's not guaranteed to happen.
- The operating system decides when each of our threads gets scheduled to execute, and depending on the timing of that, it can lead to problems.
- If Olivia puts down the chopsticks to release her lock on the critical section, but my thread doesn't get a chance to acquire them before she takes them again, then I'll be stuck waiting again, until she takes another piece.
- If that happens occasionally, it's probably not a big deal. But if it happens regularly. Then my thread's going to starve.
- **Starvation occurs when a thread is unable to gain access to a necessary resource, and is therefore unable to make progress.**
- If another greedy thread is frequently holding a lock on the shared resource, then the starved thread won't get a chance to execute.
- In a simple scenario like ours, with two equal threads competing for execution time, starvation probably isn't a concern. Both of our threads should get plenty of chances to take sushi.
- However, if our two threads are given different priorities, then that may not be the case. Baron knows I can get grumpy when I don't eat. so Olivia's thread will have a higher priority.
-  How different thread priorities get treated will depend on the operating system.
  - But, generally, higher priority threads will be scheduled to execute more often and that can leave low priority threads like me feeling hungry.
- Another thing **that can lead to starvation is having too many concurrent threads. **
