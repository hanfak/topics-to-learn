# Cache

## What?

-  technique to speed up performance in a system.  Thus caching helps to reduce "latency" in a system.
- Example
  -  we use caching as a matter of common-sense (most of the time...). If we live next door to a supermarket, we still want to buy and store some basics in our fridge and our food cupboard.  This is caching.
  - We dont need to go to the supermarket all the time (Takes too long), so we store something close by
  - When the food is finished, or out of date, we go back to the supermarket

## How ?

- Store some data, as a key-value pair
  - This can be in memory using hashmap
  - An external service (distributed caching) so multiple users of this cached data is always in sync
  - Any medium that is faster than calculating or getting the data from
    - instead of network call, the cache medium can be a database
    - instead of database, it can be a file on the same server
- This data in a cache needs to be updated, as it can become out of date or it is updated, when to do this and techniques are numerous

## When to use?

- Generally, caching works best when used to store static or infrequently changing data, and when the sources of change are likely to be single operations rather than user-generated operations.
- if we end up relying on certain pieces of data often, we may want to cache that data so that our app performs faster.
  - This is often true when it's faster to retrieve data from Memory rather than disk/services because of the latency in making network requests.
  - Example
    - many websites are cached (especially if content doesn't change frequently) in CDNs so that it can be served to the end user much faster, and it reduces load on the backend servers
- where your backend has to do some computationally intensive and time consuming work. Caching previous results that converts your lookup time from a linear O(N) time to constant O(1) time could be very advantageous.
- if your server has to make multiple network requests and API calls in order to compose the data that gets sent back to the requester, then caching data could reduce the number of network calls, and thus the latency.
- If your system has a client (front end), and a server and databases (backend) then caching can be inserted on the client (e.g. browser storage), between the client and the server (e.g. CDNs), or on the server itself. This would reduce over-the-network calls to the database.
- To reduce load on database or network service
- Can and does occur in hardware, cpu cache

## Why use?


## When not to use?

- Where consistency and freshness in data is critical, caching may not be an optimal solution, unless there is another element in the system that efficiently refreshes the caches are intervals that do not adversely impact the purpose and user experience of the application.
- Data changes all the time, so need to make the expensive call
  - Data can be changing and updating cache, and if this happens to fast then cache might be out of date
- If using distributed caching, then consistency will be an issue
- Cannot just add lots of data into cache because
  - hardware is more expensive
  - it cache service or app with intenal cache goes down, you will lose all data in cache, thus refilling will take time
  - More data will lead to increased search times, hence it would be better to use the database/sevice instead


## Location of cache

- Nearer the app
  - Faster
  - simpler
  - it will use up the memory assigned to the app
    - Will not provide more resources to the app (increase cost)
  - If server fails, the cached data is lost
  - If replicas have their own cache then they may not be in sync (not consistent), so different results if hitting different servers

- Nearer the database/service
  - Use of a global cache (distributed)
  - Faster then hitting database or network
    - no computation, faster network call (close to the server), better technology(algorithm) that handles data consistency
  - Redis

## Types of caches

- Memoization

## Write operations

- Write operations are not too different from read operations
- Considerations:
  - write operations require keeping the cache and your database in sync
    - this may increase complexity because there are more operations to perform, and new considerations around handling un-synced or "stale" data need to be carefully analyzed
  - new design principles may need to be implemented to handle that syncing
    - should it be done synchronously, or asynchronously?
    - If async, then at what intervals?
    - Where does data get served from in the mean time?
    - How often does the cache need to be refreshed, etc...
  - data "eviction" or turnover and refreshes of data, to keep cached data fresh and up-to-date. Techniques like:
    - Last in first out (LIFO) or First in last out (FILO)
    - First in first out (FIFO)
    - Least recently used (LRU)
    - Least-frequently used (LFU)

## Policies

- https://en.wikipedia.org/wiki/Cache_replacement_policies

### types cache replacement policy

when cache is full

- LRU
- https://en.wikipedia.org/wiki/Cache_replacement_policies

### cache update

when cache contents are too old, or updated elsewhere and needs to be replaced with new version

### cache writing policy

when cache contents needs to be written to backing store ie db

## Distributed caching
