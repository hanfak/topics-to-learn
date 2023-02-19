# Server Sent Events

- one request, but the response is very long, never ending
- client can handle and parse this response
  - spot the chunks and initiate some code
- Using content-type: Chunk-stream or event-stream
- Designed for http and req/resp
- overcomes issues of push

## What

- A response has start and end
- Client sends a request
- Server sends logical events as part of response
  - event has a start and end which the client can recognise and unfold to use
- Server never writes the end of the response
- It is still a request but an unending response
- Client parses the streams data looking for events
- Works with request/response (HTTP)

## PRo

- real time
- Compatible with req/resp

## Cons
- Client must be online
- Might not be able to handle all these events
  - similar to push
  - client might disconnect
  - The server will have to handle this problem
- polling is preferred for lighter clients
- Using http 1.1 issue
  - can only make 6 connections to a domain
  - only one request per connection, and until the request is finished cannot send anything else on that connection
  - so if all 6 req are server side events, it will be  blocked
- Better to use http2
  - can send multiple streams in same connnection
