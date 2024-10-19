# Optimistic vs Pessimistic Concurrency

- used in situations to maintain data consistency, when multiple multiple actions happen at the same time

## Optimistic Concurrency

-  considers the best scenario when handling concurrency
- assumes that conflicts between transactions will happen infrequently and allows transactions to happen in an unsynchronised manner without any interference
- No blocking or locks
  - Can scale better, and better availability
  - Allows for high levels of concurrency
- USeful for read heavy loads
- No deadlocks
- Checks will happen at point of commiting transactions
  - if conflicts, then user will have to fix
- Disadvantage
  - manual intervention
  - Cost of rollbacks and retries
  - maintain versioning/timestamps
- The repeatable read is more strict isolation level in that it has the same guarantees as read committed isolation, plus it guarantees that reads are repeatable.
  - A repeatable read guarantees that if a transaction reads a row of data, any subsequent reads of that same row of data within the same transaction will yield the same result, regardless of changes made by other transactions
  - 
- Implementation
  - use of timestamp or version number, and use this to compare transactions and which to keep
  - For version number
    - new column in db
    - On creation of record/row, is set to 1
    - On update incremented by 1, only if the version is expected (ie 1), else discard or retried

## Pessimistic Concurrency

- assumes that conflicts between transactions can happen often and blocks data records when a user starts to update
- Involves blocking other users trying to mutate the same thing
  - involves locks
  - Other users can mutate only after the lock has been released
- Locks used
  - shared
    - Allows other users to read the data record, but they can't update it.
  - Exclusive
    -  Only the user who applied the lock can read or update the data record. No other locks can be applied until the user releases the lock.
  - Update
    - only the user who applied the lock can read or update the data record. 
    - users can apply update locks when another user already has a shared lock.
- Not great for scaling
- Need to keep locking to minimum ie fixed time to complete (timeouts)
- Deadlocks can happen
- Enforces consistency
- High resource usage for locks and wait time
- Prevent dirty writes
  - dirty write is
    - Overwriting data that has already been written by another transaction but not yet committed
- PRevent dirty reads
  - dirty read is
    - Reading data from another transaction that has not yet been committed
  - Via read/write locks
  - 
- Can use `Select for update` via database
  - which creates a lock on that row
  - disable autocommit before
  - Run update/s
  - release lock (for db this can be on commit/rollback/disconnect)

## Links 
- https://www.freecodecamp.org/news/how-databases-guarantee-isolation/
- https://learn.microsoft.com/en-us/dotnet/framework/data/adonet/optimistic-concurrency