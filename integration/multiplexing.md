# Multiplexing & Demultiplexing

- More to do with networking
- Used in many protocols - http2, quic, mptcp

## What

- Multiplexing
  - taking several lines (requests) and merging them into one
  - reduce number of tcp connections
  - Done on client side
- Demultiplexing
  - is the reverse
  - taking one line which contains multiple messages/requests and spliting the out into separate requests
  - Done on the server side, thus each request can be handled separately

## Example - Connection pooling

- Creation of multiple connections to a database, keep them hot never closed, and allow the code to use a free one instead of creating on the fly (which is expensive) or having one connection which leads to contention; and release it back to the pool for others to use when done.
  - If a new req comes in and needs a connection, but all the connections are used in the pool, it will be blocked until one is free  
-   

## Why

- Common example of http1.1 and browsers, if a website needs to make several requests to different endpoints, it will need to make several unique tcp connections. But the browsers only allow a max of 6 tcp connections, so there will be some wait time.
  - Using Http 2, the reques is multiplex so can send multiple req in a single tcp connections (within reason)

## Issues

- When the single multiplexed request is demultiplexed then it puts strain on the cpu
