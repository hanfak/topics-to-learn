#  Conflict-free Replicated Data Type

- data structure that simplifies distributed data storage systems and multi-user applications.
- copies of some data need to be stored on multiple computers
  - the data may be concurrently modified on different replicas.
  - Can be handled:
    - Strongly consistent replication
      - the replicas coordinate with each other to decide when and how to apply the modifications
      - enables strong consistency models such as serializable transactions and linearizability
      - waiting for this coordination reduces the performance of these systems
    - Optimistic replication
      - users may modify the data on any replica independently of any other replica, even if the replica is offline or disconnected from the others.
      - enables maximum performance and availability, but it can lead to conflicts when multiple clients or users concurrently modify the same piece of data.
      - conflicts then need to be resolved when the replicas communicate with each other.
- Conflict-free Replicated Data Types (CRDTs) are used in systems with optimistic replication, where they take care of conflict resolution
  - ensure that, no matter what data modifications are made on different replicas, the data can always be merged into a consistent state.
  - merge is performed automatically by the CRDT
  -  support decentralised operation: they do not assume the use of a single server, so they can be used in peer-to-peer networks and other decentralised settings

## Links 

- https://crdt.tech/
- https://arxiv.org/pdf/1805.06358.pdf
- https://inria.hal.science/inria-00555588/document