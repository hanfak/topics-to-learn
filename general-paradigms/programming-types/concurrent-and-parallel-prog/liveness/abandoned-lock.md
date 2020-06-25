# Abandoned Lock

- another form of a deadlock through thread death.
- If one thread or process acquires a lock, and then terminates because of some unexpected reason, it may not automatically release the lock before it disappears.
- That leaves other tasks like me stuck waiting for a lock that will never be released and getting hungry.
