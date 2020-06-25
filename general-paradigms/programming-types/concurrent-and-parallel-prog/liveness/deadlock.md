# Deadlocks

- A classic example that's used to illustrate synchronization issues when multiple threads are competing for multiple locks is the dining philosophers problem.
  - In this scenario, Olivia and I are two philosophers, or threads, doing what philosophers do best, thinking and eating. We both need to access a shared resource, this plate of sushi, and each time one of us takes a piece of sushi, we're modifying its value, the number of pieces that are left. The act of taking sushi from the plate is a critical section, so to protect it, we've devised a mutual exclusion process using these two chopsticks as mutexes. When I want to take a bite of sushi, I'll first pick up the chopstick closest to me to acquire a lock on it, then I pick up the farther chopstick. Now I have possession of both locks. I'm in the critical section, so I'll take a piece of sushi and then put down the far chopstick to release my lock on it, and then the close chopstick. And finally, since I'm a philosopher, I'll go back to philosophizing.
  - Second philosopher: Ah, eureka. That was an interesting thought. Well, I'm feeling hungry now, so I'll acquire the chopstick closest to me and then the one further away. I'll take a piece of sushi, and then release the far chopstick and then the one closer to me.
  - As standing philosophers, we'll both continue to alternate between eating and thinking, but since we're operating as concurrent threads, neither one of us knows when the other one wants to eat or think, and that can lead to problems.
  - If I get hungry again and pick up the chopstick closest to me and the other philosopher also get hungry and pick up my close chopstick, I see we've come to an impasse.
    - We've both acquired one of the two locks that we need, so we're both stuck waiting on the other thread to release the other lock to make progress.
- **This is one example of a situation called deadlock. Each member of a group is waiting for some other member to take action, and as a result, neither member is able to make progress.**
- Avoiding deadlock is common challenge in concurrent programs that use mutual exclusion mechanisms to protect critical sections of code.
- We want our program to be free from deadlock to g**uarantee liveness, which is a set of properties that require concurrent programs to make progress**.
- Some processes or threads may have to take turns in a critical section, but a well-written program with liveness guarantees that all processes will eventually make progress.
-  Well, our deadlock occurred because we both reached for the chopstick closest to us first. I grabbed this chopstick first, and you grabbed this chopstick first. That set us up for a deadlock.
  - But **if we prioritize these locks so that we both try to acquire this chopstick first, then we won't have this problem because we'll both be competing for the same first lock**.  If you acquire the first chopstick and then I try to acquire it, I'll just be stuck here waiting until you finish taking your sushi and release both locks. Then I can grab that chopstick and this one, and take my turn in the critical section.
  - In this example, we had two separate locks protecting a single shared resource. That may not be the most realistic scenario, but it demonstrates the point.
- Now, imagine something like a banking application with a set of bank accounts where each one has its own mutex to ensure that only one thread will be withdrawing from or depositing funds to that account at time. To transfer funds between two accounts, a thread needs to acquire the locks for both the sender and the receiver since it would be modifying the value of both accounts. If there are multiple threads concurrently making transfer between the accounts, then there's a real chance that they could end up competing for the same locks and run into this sort of deadlock scenario.

## Solution

- as your programs grow in complexity to include more critical sections, locks, and parallel threads with intertwined dependencies, it becomes increasingly more difficult to identify and prevent potential Deadlocks.
- to ensure that locks are always taken in the same order by every thread
- Put a time out on locking attempts
  -  If a thread is not able to successfully acquire all of the locks it needs within a certain amount of time it will back up, free all of the locks that it did take, and then wait for a random amount of time before trying again to give other threads a chance to take the locks they need.
