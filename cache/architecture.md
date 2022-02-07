# Caching Architecture

##  Embedded Cache

- most common
- Copy of data (from db, expensive io call, or expensive calculation) put in memory
- Common with cpu and l4 cache
- Within applications, this is just a map/dictionary

## Client-Service Cache

- cache is placed outside of application and is placed between app and the other system
- Proxy
- Having multiple apps or replicas that talk to the cache instead

## Distributed Cache

- Instead of having one cache, will have multiple caches, to increase avialability of cache, or locate cache closer to consumer
- low latency high volume

## Cloud Cache or CSP Managed Cache

- distributed cache that is managed by cloud provider
- Dont need to manage it
- improve scalability

## Reverse-Proxy Cache

- responses cached
- GET requests
- cache stored inside the proxy
- avoids bombarding servers

## Side-car Cache

- The cache is attached to container running in the pod
- cache per replica
- lifecycle tied to the pod
- low latency
- app and data isolation

## Reverse-Proxy Side-car Cache
