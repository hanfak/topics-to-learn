# Distribution strategies

- NOTE: PEAA has a lot of outdated ideas, and tech and techinques have changed

## What

- Distributed processing is done by placing objects on different nodes(processes on different machines connected via networks)
- Benefits
  - load can be distributed between different nodes, better performance ie throughput
  - Easier to add nodes (horizontal scaling and load balancing needed)
  - Calls between nodes are transparent and easy to follow
- Dont distribute if you dont have to
  - This is not the case for a lot of cases, apart from fast performance requirements. As the benefits of distributing (see micros services) can out way the costs
  - Does apply to objects, this pattern has been deprecated (ie COBRA, DCOM etc). Instead use of messaging protocols, rest with json/xml, grpc are used now. 

## Types
- Local call
  - calls between components on the same node
  - very fast
- Remote call
  - calls between components on different machines
  - Calls need to be course grained
    - minimise remote function calls
  - slower
    - marshall and unmarshal data
    - data transfer over network (latency and unreliability/partitioning)
  - Now speed of calls of fast, so do a few does not matter, but if dealing lots of calls, despite the speed of the response, the law of big numbers will see slow down
- OOP
