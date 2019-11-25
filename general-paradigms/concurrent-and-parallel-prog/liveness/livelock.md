# Livelock

-  A livelock looks similar to a deadlock in the sense that two threads are blocking each other from making progress, but the difference is that the **threads in a livelock are actively trying to resolve the problem**.
- A livelock can occur when two or more threads are designed to respond to the actions of each other.
- Both threads are busy doing something, but the combination of their efforts prevent them from actually making progress and accomplishing anything useful. The program will never reach the end.
- The ironic thing about livelocks is that they're often caused by algorithms that are intended to detect and recover from deadlock. If one or more processor thread takes action to resolve the deadlock, then those threads can end up being overly polite and stuck in a livelock.
-  **To avoid that, ensure that only one process takes action chosen by priority or some other mechanism, like random selection**.
