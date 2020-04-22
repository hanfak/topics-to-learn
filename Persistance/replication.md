# Replication and Sharding

## What

- Replication means to duplicate (make copies of, replicate) your database.
- Replication ensures redundancy in the database if one goes down. But it also raises the question of how to synchronize data across the replicas, since they're meant to have the same data.
- Replication on write and update operations to a database can happen synchronously (at the same time as the changes to the main database) or asynchronously .
- The acceptable time interval between synchronising the main and a replica database really depends on your needs - if you really need state between the two databases to be consistent then the replication needs to be rapid
  - You also want to ensure that if the write operation to the replica fails, the write operation to the main database also fails (atomicity).
- what do you do when you've got so much data that simply replicating it may solve availability issues but does not solve throughput and latency issues (speed)?
  - consider "chunking down" your data, into "shards". Some people also call this partitioning your data (which is different from partitioning your hard drive!).
  - Sharding data breaks your huge database into smaller databases.  You can work out how you want to shard your data depending on its structure.  It could be as simple as every 5 million rows are saved in a different shard, or go for other strategies that best fit your data, needs and locations served.
