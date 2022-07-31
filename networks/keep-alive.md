# Keep alive

- Is a setting in http, that allows the consumer (typically a browser) to reuse the same original tcp connection to make several http request/response
- This setting only asks the server to keep alive the connection
- Is a form of multiplexing
- Generally, there is a timeout to reconnect with a new tcp connection
  - in firefox
    - network.http.keep-alive.timeout = 0, this will stop the use of keep-alive
    - network.tcp.keepalive.enabled
  - There is also a MaxKeepAliveRequests, to limit the number of requests a tcp connection should handle before getting an new tcp connection
  - part of the headers of the http request (http 1.0)
    - `Connection: keep-alive; Keep-Alive: timeout=5, max=1000`
- Prohibited in http 2.0
- For http 1.1 keep-alive is default

## Pros
- This saves having to do a whole new connection, handshake and tls stuff, thus reducing the RTT
- Network resource conservation – It’s less taxing on network resources to use a single connection per client.
- Reduced network congestion – Reducing the number of TCP connections between your servers and clients can lead to a drop in network congestion.
- Decreased latency – Reducing the number of three-way handshakes can lead to improved site latency.


## ISsues

- Having high timeouts or max requests, can use resources for too long running multiple server processes or threads.
- Servers may not conform to keep-alive, if their servers are under stress
- For some low-frequency access resources / services, such as a cold image server, less than a few times a year, it is wasteful to keep the next connection (this scenario is not very appropriate). Keep alive may have a great impact on performance, because it keeps unnecessary connections for a long time after the file is requested, which takes up the number of connections on the server side.
## Links

- https://reqbin.com/req/java/4sa9kqvu/keep-alive-connection-example#:~:text=The%20Keep%2DAlive%20Connection%20means,request%20header%20to%20the%20server.
- https://stackoverflow.com/questions/13677261/how-to-keep-httpclient-connection-keep-alive
- https://developpaper.com/talking-about-the-keep-alive-mechanism-in-http-and-the-keep-alive-mechanism-in-java-http/
