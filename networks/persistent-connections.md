# Persistent Connection

- refers to a long-lived connection between a client and a server that remains open for an extended period, allowing multiple requests and responses to be sent without establishing a new connection for each interaction
- Typically occurs in websockets 
- keeping the connection open for an extended duration, persistent connections offer several advantages. 
  - They eliminate the need to establish a new connection for each request, reducing the overhead associated with repeated handshakes. 
  - This approach also enables real-time and interactive communication between the client and server, making it well-suited for applications that require instant updates and bidirectional data transfer.
- Can occur via http 
  - keep-alive connections, where the server keeps the TCP connection open for multiple HTTP requests and responses within a certain timeframe. 