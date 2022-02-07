# Replication and Sharding

## What

- Replication means to duplicate (make copies of, replicate) your database.
  - Common terms include master-slave, leader-follower, primary-secondary
- Replication ensures redundancy in the database if one goes down. But it also raises the question of how to synchronize data across the replicas, since they're meant to have the same data.
- Helps with latency, if primary db is in USA, and secondary db is in UK, then the uk service should use the db in UK instead of USA to reduce network speed
  - But will need to wait for the uk db to synchronised with USA db
- Replication on write and update operations to a database can happen synchronously (at the same time as the changes to the main database) or asynchronously .
- Replicas can handle different operations
  - if read heavy, then replicas can be read only, and the primary db can be write/read. Thus one source of truth, but need to wait for all db to be sync
  - if write db goes down, another db can take over as the write db
- The acceptable time interval between synchronising the main and a replica database really depends on your needs - if you really need state between the two databases to be consistent then the replication needs to be rapid
  - You also want to ensure that if the write operation to the replica fails, the write operation to the main database also fails (atomicity).
- what do you do when you've got so much data that simply replicating it may solve availability issues but does not solve throughput and latency issues (speed)?
  - consider "chunking down" your data, into "shards". Some people also call this partitioning your data (which is different from partitioning your hard drive!).
  - Sharding data breaks your huge database into smaller databases.  You can work out how you want to shard your data depending on its structure.  It could be as simple as every 5 million rows are saved in a different shard, or go for other strategies that best fit your data, needs and locations served.

##

## Lag

- The time taken for data to be copied from DB to it's replica
- If update happens, and lag is slow, the reading data from replicas will give consumers stale data, or inconsistent date if sync data happens on a few of the db replicas

### Fix synchronously

- Read after write consistency
  - blocks any queries if a write is progress and syncing with replicas
  - The issuer of the write, will only get confirmation when the data is inserted and replicated to all replicas
  - Lag is zero
  - Data is always consistent
  - performance might take a hit
  - If one of the replicas is down, then the write will never be completed, system will be indefinitely blocked until that replica is backup and synched
    - or it is terminated, and a rollback is issued to previous state (increase time)

### Fix asynchronously

- Once the write has been done in the primary db, an update is sent concurrently to all replicas  (fire and forget) not waiting for acknowledgemetn that it was complete, when all updates are sent, the issuer of the write is informed of completion.
- Eventual consistency
- faster
- if a replica fails, the state will be in in complete
  - can fix by using a quorum of replicas to decide what the actual value should be when a query is asked for

### Semi synchronous

- Same as async model, but it waits for at least one (or a quorum of replicas) to acknowledge synchronisation  before confirming with user

## Which to use

- Depends on what is important
- consistency but slow and unavailable or fast but inconsistent 

## Links
- https://youtu.be/RIcNswROzCc
