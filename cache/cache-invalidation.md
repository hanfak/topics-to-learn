# Cache Invalidation and Eviction

r- Data stored in cache is not there forever, it can become stale (not correct)
  - The data needs to invalidated, evicted and replaced
- Cache invalidation, is the process where the data is updated or removed from the cache

## TTL - Time To Live

- This is time value, which stored along with the cached data
- When the TTL expires it will either remove the data or update it
- Having a very low TTL, means that the cache is updated frequently, and you lose the performance benefit of a cache and possibly overload the system
- Have a large TTL, leads to stale data being used
- Finding the TTL, can be very hard, requires investigation and metrics

## On update

- This updates the cache at the same time data source is updated

## least recently used (LRU)

- invalidate the data which was least used

## least frequently used (LFU)
- keeps the most frequently used data

## First in first out

- treat as queue

## Freshness caching verification
- where the application executes a lightweight procedure to determine if the data is still valid every time the data is retrieved. The downside of this alternative is that it produces some execution overhead

## Active application invalidation
- where the application actively invalidates the data in the cache, normally when some state change is identified.
