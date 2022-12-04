# Concurrency



## Definitions

- Concurrency occurs when different processes or applications need the same resource to continue to work.
- When computations overlap in time and which may permit the sharing of a common resource (ie memory) between those overlapped computations
- Systems must support many simultaneous users
  - need to guarantee correctness

## Issues

- It is hard, due to number of possibilities of order of executions
  - Hard to test
  - Hard to debug
- Let others handle it and dont think about it, like transaction managers
  - When all actions that need to occur happen in a transaction, nothing bad happens
  - But not all actions can be placed in a transaction, especially database transactions
- Ignored about

## Execution contexts

- Processing always occurs in some kind of context, usually more than one.
- An enterprise application will usually have Requests and Sessions both as a server to clients and as a client to other applications like a DB server or a 3rd party application API.
- Application servers where supporting multiple threads in an application server system.

### Definitions

- Request
  - A single short term call from the outside world to the application, which may result in it returning a response
  - During a request the processing is largely in the server's court and the client is assumed to wait for a response.
    - This could be a message and client may not need to wait for the processing on the server to finish
  - More often a client may issue another request that may interfere with one it just sent.
    - So a client may ask to place an order and then issue a separate request to cancel that order.
    - From the client's view the two requests may be obviously connected, but depending on your protocol that may not be so obvious to the server.
- Session
  - A long running interaction between client and server, usually consisting of a series of requests.
  - ie loggin in, doing multiple actions, logging off on purpose or via timeout
- Process
  - A heavyweight context that provides isolation to the data it works on.
- Thread
  - A lightweight context that is set up so that several threads are ran in a single process.
  - They support multiple requests in a single process, helping to make good usage of resources.
  - However, because they run in a single process, they share memory, which leads to concurrency problems.
- Transaction
  - A transaction groups together several Requests that the application wants to treat as a single Request.
  - We can have system transactions (ie. connecting to a DB) or business transactions (ie. a user interacting with the application)

### Issues

- Not all context line up perfectly
- In theory each session would have an exclusive relationship with a process for its whole lifetime
  - Since processes are properly isolated from each other, this would help reduce concurrency conflicts
  - But this does not exists
  - Alternatively, start a new process for each request
    - but bad as ties up a lot of resources on one machine
    - but good for multi cores or microservices ie replicas

## Concurrency problems

- Concurrency problems occur when more than one active agent, such as a process or thread, has access to the same piece of data
- Concurrency solutions tries to solve these issues
- inconsistent reads and lost updates
- failure of correctness/safety
  - result in incorrect behavior that would not have occurred without two people trying to work with the same data at the same time
- it's not enough to worry about correctness;
  - have to worry about liveness: how much concurrent activity can go on.
- Often people need to sacrifice some correctness to gain more liveness
- The solutions lead to other problems

### Inconsistent reads

-  when you read two things that are correct pieces of information but not correct at the same time.
- when  a user reads some data and that data is changed by another user while he is still using the data.
  - The data he read and is still using, is then inconsistent.
- Solution
  - Pessimistic lock solution
    - Using a pessimistic lock we need to acquire a shared lock for reading and an exclusive lock for writing. However, the rules to acquire a lock are:
      - Any number of shared locks can be acquired at any given time, as long as there is no exclusive lock acquired.
      - An exclusive lock can be acquired at any given time, as long as no other lock (shared or exclusive) has been acquired.
  - Optimistic lock solution
    - With an optimistic lock, every piece of data has a version tag on it.
    - When making an update, the system checks for differences in data versions. If a difference is detected, a conflict is raised.

### Lost updates

- When two or more users update the same resource (ie file) but one saves before the other user saves their update before the first user, the first user does not get this update and saves, so the resource does not include both updates

## Race conditions

- When 2 or more users are updating that same data, a race condition can occur causing corrupt data

## Isolation and Immutability solutions

- Solve concurrency problems

### isolation

- Partition the data so that any piece of it can only be accessed by one active agent.
- arrange things so that the programs enters an isolated zone, within which you don't have to worry about concurrency
- Processes work like this in operating system memory
  - The operating system allocates memory exclusively to a single process, and only that process can read or write the data
  - file locks, once open no one else can update it, but multiple users can open read only copies
- Good
  - Reduce errors

### Immutability

- Avoids all concurrency problems
- Cannot make everything immutable, as most systems is designed to mutate data
-  by identifying some data as immutable, or at least immutable almost all the time
-  separate applications that are only reading data, and have them use copied data sources, from which we can then relax all concurrency controls

## Optimistic and Pessimistic Concurrency Control

- USed when cannot isolate mutable data
- Forms of locking
- Can cause a set of different problems

### Optimistic

- A copy is made for each user. The first to finish commits update as normal, the following users to commit must handle the conflicts between their changes and previously saved changes from the same copy. Once resolved then can commit
- Git  
- About conflict detection
- lock held during the commit
- Good
  - Can increase concurrency
- Bad
  - How to handle conflicts, as it will probably need tooling or manual intervention
  - How to do with business data

### Pessimistic

-  whoever checks out the file first prevents anyone else from editing it.
- about conflict prevention
- Bad
  - prevents concurrency, everyone must wait, bottle neck

### Preventing inconsistent reads

-  easy to miss because most people tend to focus on lost updates as the essential problem in concurrency
-  Pessimistic locks have a well-worn way of dealing with this problem through read and write locks.
  - To read data you need a read (or shared) lock; to write data you need a write (or exclusive) lock.
  - Many people can have read locks on the data at one time
  - if anyone has a read lock nobody can get a write lock
  -  once somebody has a write lock, then nobody else can have any lock.
- Optimistic locks
  - use some form of version marker on the data
  - timestampe or sequential counter
  -  To detect lost updates the system checks the version marker of your update with the version marker of the shared data.
    - If they're the same, the system allows the update and updates the version marker
  - In this case every bit of data that was read also needs to have its version marker compared with the shared data. Any differences indicate a conflict.
  - Bad
    - Controlling access to every bit of data that's read often causes unnecessary problems due to conflicts or waits on data that doesn't actually matter that much
      - Fix - separating out data you've used from data you've merely read.
    - Figuring out what needs to be controlled and not is tough
- Temproal Reads
  - These prefix each read of data with some kind of timestamp or immutable label, and the database returns the data as it was according to that time or label.
  - similar to event sourcing
  - Bad
    - data source needs to provide a full temporal history of changes, which takes time and space to process
    - difficult for databases

### Deadlocks

- Issue with Pessimistic locking
- Multiple users need access to another users file which is under going change. But everyone has a lock on that file. Cannot release the lock until all their changes are done. And their wont be done unless they change the file which has a lock. Neither can make progress until the other completes
- happens when two processes have locks on different resources and suddenly they both require each others locked resources in order to finish their job and releasing their lock. This means they would both be waiting for each others locks to be released.
- Fix
  - Have an external detector, which picks a victim(s) who have to give up their lock so others can progress
    - The victims(s) changes will be lost
    - It is hard to detect
  - Give all locks a timeout
    - Once you hit that limit you lose your locks and your work—essentially becoming a victim.
    - This can cause victims to lose changes, when no deadlock has occurred
  - Prevent from happening at the start
    - Deadlocks occur when people who already have locks try to get more or to upgrade from read to write locks.
    - Is to force people to acquire all their locks at once at the beginning of their work and then prevent them gaining more
      - ie get locks on files in alphabetical order
    - If lock is already taken, then this new user becomes victim
  - Automatic victim
    - when a process tries to acquire a lock on an already locked resource, it automatically becomes a victim.
  - mix
- Best to use timeout and getting all locks at the beginning

## Transactions

-  what guarantees that a sequence of actions are all successfully and fully executed, or none is.
- Bounded sequence of work
- All participating  resources are in a consistent state before and after the transaction
- Must have ACID properties
- Primary tool for handling concurrency
- Example
  - ATM transaction, till you get the money out of the ATM machine, your amount of money in your account value will be same.

### ACID

#### Atomicity

- All actions in a transaction are guaranteed to complete successfully or none is executed
- If not completed successfully then all steps must be rolled back
- There is no such idea of partial completion
- Committing is the act of saying all steps in the transaction have happened and confirmed

#### Consistency

- A system resources must be in a consistent, non corrupt state at the start and end of a transaction.

#### Isolation

- The result of a transaction is only visible when the whole transaction is finished.

#### Durability

- The result of a transaction must be permanent.

### Transactional Resources

- to mean anything that's transactional
  - that uses transactions to control concurrency
- Transactions generally occur with databases
  - others queues, printers, atm
- Higher throughput means transactions must be short as possible
  - This is a request transaction
  - should not span multiple requests
  -  a common approach is to start a transaction at the beginning of a request and complete it at the end.
  - Modern systems use AOP and annotations tag methods as transactions
- Long transactions are transactions that span multiple requests
- Late transaction
  - Do all the reads outside of a transaction, then only start the transaction when doing the updates
  - If there's a lengthy time lag between the opening of the transaction and the first write, this may improve liveness.
  - can lead to inconsistent reads
  - not worth doing, unless have heavy contention
- Be aware of locks
  - Many db locks the rows involved to allow multiple transactions on the same table
  - if a transaction locks a lot of rows in a table, then the database has more locks than it can handle and escalates the locking to the entire table—locking out other transactions.
  - This lock escalation
### Reducing Transaction Isolation for Liveness
-  If you have full isolation, you get serializable transactions.
- Transactions are serializable if they can be executed concurrently and you get a result that's the same as you get from some sequence of executing the transactions serially.
-  serializability guarantees that he gets a result that corresponds to completing his transaction either entirely before another transaction starts or after it finishes
-  Serializability can't guarantee which result, as in this case, but at least it guarantees a correct one
- Serializability is strongest level of isolation
  - defines correctness
  - reduces liveness
  - might need to reduce serializability to increase through put
- repeatable read
  - Allows phantoms
    - Phantoms occur when you add some elements to a collection and the reader sees only some of them
    - always things that are inserted
- read committed
  - allow unrepeatable reads and phantoms
  - read before another transaction gives one value, afterwards the same read will give different value that has been affected by the transaction
  - It's easier for databases to spot unrepeatable reads than phantoms, so the repeatable read gives you more correctness than read committed but less liveness.
- read uncommitted
  - lowest level of isolation
  - allows dirty reads, unrepeatable reads and phantoms
  - you can read data that another transaction hasn't actually committed yet
  - Two errors
    - user a might look at the locking package when user b adds the first of his files but before he adds the second. As a result he sees n + 1 files in the locking package, instead of the final outcome n + 2 files
    - user b adds his files but then rolls back his transaction, thus user a sees files that were never really there

### Business and system transactions

- A database transaction is a group of SQL commands delimited by instructions to begin and end it.
  - If the fourth statement in the transaction results in an integrity constraint violation, the database must roll back the effects of the first three statements and notify the caller that the transaction has failed.
  - If all four statements had completed successfully all would have been made visible to other users at the same time rather than one at a time.
-  to supporting the ACID properties of a business transaction is to execute the entire business transaction within a single system transaction
-  business transactions often take multiple requests to complete, so using a single system transaction to implement one results in a long system transaction.
  - Most transaction systems don't work very efficiently with long transactions.
  -  the application won't be scalable because long transactions will turn the database into a major bottleneck
  - refactoring from long to small transactions is hard
- Business transactions need to be done as short transactions, and done at the beginning
  - Thus ACID properties are handled by the system rather than in the database
  - Called Offline Concurrency
- Business transactions are closely tied to sessions. In the user's view each session is a sequence of business transactions (unless they're only reading data), so we usually make the assumption that all business transactions execute in a single client session


### Types

- Long transaction
  - Spans several requests
- Request transaction
  - Always starts in the beginning of a request and finishes in the end of the request.
- Late transaction
  - As a request transaction, but it is open as late as possible, allowing the reads to be made outside of the transaction.
- System transaction
  - A transaction that operates at the infrastructure level, usually when communicating to the DB.
- Business transaction
  - A transaction that operates at a use case level, ie. encompasses several user screens from the beginning of the use case flow until its end.



## offline concurrency,

- concurrency control for data that's manipulated during multiple database transactions.

## Application Server Concurrency

## Locking

- To avoid problems of lost updates or inconsistent reads, need to lock access to the shared data
- Why
  - provides correctness
  - reducess concurrency
  - only one person/thread can work on the data at the same time
- Bad
  - Liveness suffers
    - Reduce the number of concurrent activity occurs
    - as the lock creates a bottle neck where other threads must wait to finish and release the lock

### Optimistic Offline Lock
### Pessimistic Offline Lock
### Coarse-Grained Lock
### Implicit Lock
