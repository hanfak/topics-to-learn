# Cache Patterns

- https://codeahoy.com/2017/08/11/caching-strategies-and-how-to-choose-the-right-one/
- https://www.youtube.com/watch?v=Ez1GK2imrsY

## Cache aside

- The application first checks the cache.
- If the data is found in cache, we’ve cache hit. The data is read and returned to the client.
- If the data is not found in cache, we’ve cache miss. The application has to do some extra work. It queries the database to read the data, returns it to the client and stores the data in cache so the subsequent reads for the same data results in a cache hit.
- best for read-heavy workloads.
- If the cache cluster goes down, the system can still operate by going directly to the database.
- the data model in cache can be different than the data model in database. E.g. the response generated as a result of multiple queries can be stored against some request id.
-  the most common write strategy is to write data to the database directly. When this happens, cache may become inconsistent with the database. To deal with this, developers generally use time to live (TTL) and continue serving stale data until TTL expires. If data freshness must be guaranteed, developers either invalidate the cache entry or use an appropriate write strategy
- If update to db happens and cache has a value for this, then the consumer will get a stale data
  - To avoid, the cache value needs to be invalidated (removed or updated) when a write happens to the DB
- Advantage
  - If db goes down, the app can still serve data using the cache
    - although could be stale data
  - If cache goes down, then all reqeusts will go to DB, but will be slower

## Read Through strategy

- Cache sits between app and DB
  - App never talks to DB
- Acts as a proxy
- On first request to app, there is a cache miss, the cache then goes to DB and populates it and returns values to app
- Advantage
  - For read heavy
- Disadvantage
  - Cache miss always on first call
  - Fix: Pre heat the cache with data, that is believed (using stats) to be used by the app
-

## Write through

- Similar to read through pattern
- cache sits between app and DB
- Writes are written to cache first then DB
- Disadvantage
  - extra layer of latency as have to write twice

## Write around

- Mix of using read through and cache aside
- For reads, use read through
- For writes, talk directly to the dB
- Advantages
  - save one hop when talking writing

## Write back

- cache in between app and db
- All writes are stored in cache, at some time all the writes bulk updating the db
- Advantage
  - for write heavy workloads
  - Handles db failures for sometime, if when batching to update fails to connect with db, then can retry later
- Disadvantage
  - if cache goes down before batch is written to db then all the writes are lots
- Commonly used within database products, where all writes and reads are kept in some logs/journal and intermittantly add to the disk
