# Alternatives to use before using cache

- Caching can be hard use and maintain
- Try using other methods (see section ...)
- Examples to increase performance/lower latency
  - Reduce number of proxy
  - Choose more performant serializing and deserializing payload (ie protocol buffers)
  - Use http/2, have multiple requests on the same tcp connection (reactive servers like netty)
  - For client, use same tcp connection to send requests (similar to object pooling)
  - Avoid large payloads, large queries (no select *), use pagination, if filtering/ordering do it in the db, indexes in db
  - Reduce client side processings
