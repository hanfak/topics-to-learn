# ACID - Atomicity, Consistency, Isolation, Durability

- ACID transactions are a set of features that describe the transactions that a good relational database will support
- A **transaction** is an interaction with a database, typically read or write operations.

## Atomicity

- Requires that when a single transaction comprises of more than one operation, then the database must guarantee that if one operation fails the entire transaction (all operations) also fail.
-  It's "all or nothing".
- That way if the transaction succeeds, then on completion you know that all the sub-operations completed successfully, and if an operation fails, then you know that all the operations that went with it failed.
- For example
  - if a single transaction involved reading from two tables and writing to three, then if any one of those individual operations fails the entire transaction fails.
  - This means that none of those individual operations should complete. You would not want even 1 out of the 3 write transactions to work - that would "dirty" the data in your databases!

## Consistency

- Requires that each transaction in a database is valid according to the database's defined rules, and when the database changes state (some information has changed), such change is valid and does not corrupt the data.
- Each transaction moves the database from one valid state to another valid state.
- Consistency can be thought of as the following:
  - every "read" operation receives the most recent "write" operation results.

## Isolation

- means that you can "concurrently" (at the same time) run multiple transactions on a database, but the database will end up with a state that looks as though each operation had been run serially ( in a sequence, like a queue of operations).

## Durability

- is the promise that once the data is stored in the database, it will remain so.  It will be "persistent" - stored on disk and not in "memory". 


## Links

- https://database.guide/what-is-acid-in-databases/#:~:text=In%20database%20systems%2C%20ACID%20(Atomicity,occur%20while%20processing%20a%20transaction.
