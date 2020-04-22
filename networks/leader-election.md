# Leader Election

- In a setup where multiple servers are doing much the same thing, there can arise situations where you need only one server to take the lead.
- For example,
  - you want to ensure that only one server is given the responsibility for updating some third party API because multiple updates from different servers could cause issues or run up costs on the third-party's side.
  - In this case you need to choose that primary server to delegate this update responsibility to.  That process is called leader election.
- When multiple servers are in a cluster to provide redundancy, they could, amongst themselves, be configured to have one and only one leader. They would also detect when that leader server has failed, and appoint another one to take its place.
- The really tricky part is ensuring that the servers are "in sync" in terms of their data, state and operations.
- There is always the risk that certain outages could result in one or two servers being disconnected from the others,
  - In that case, engineers end up using some of the underlying ideas that are used in blockchain to derive consensus values for the cluster of servers.
-  a consensus algorithm is used to give all the servers an "agreed on" value that they can all rely on in their logic when identifying which server is the leader.
- Leader Election is commonly implemented with software like etcd, which is a store of key-value pairs that offers both high availability and strong consistency (which is valuable and an unusual combination) by using Leader Election itself and using a consensus algorithm.
- So engineers can rely on etcd's own leader election architecture to produce leader election in their systems. This is done by storing in a service like etcd, a key-value pair that represents the current leader.
  - Since etcd is highly available and strongly consistent, that key-value pair can always be relied on by your system to contain the final "source of truth" server in your cluster is the current elected leader.


## Links

- https://en.wikipedia.org/wiki/Leader_election
