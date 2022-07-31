# Thread per connection or request model

- Thread per request will create a thread for each HTTP Request the server receives
  - Thread Per Request is faster as most web container use Thread Pooling.
  - A thread per request model is one in which a single thread is coupled to the lifecycle of a request. 
- Thread per connection will reuse the same HTTP Connection from multiple requests(keep-alive) .AKA HTTP persistent connection but please note that this supported only from HTTP 1.1

- Thread per request should be better, because it reuses threads, while some client may be idle. If you have a lot of concurrent users, they could be served with a less number of threads and having equal number of thread would be more expensive.
  - we do not know if user is still working with application, so we cant know when to destroy a thread. With a thread per request mechanism, we just use a thread pool.
