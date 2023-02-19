# Long Polling

- Request is taking long, I’ll check with you later But talk to me only when it's ready
- moving short polling from the client to the server

## Use case

- Short polling and req/resp not ideal
- Same usecase as short polling But too chatty
  - A request takes long time to process
  - The backend want to sends notification
- Kafka uses it

## How

- Client sends a request
- Server responds immediately with a handle
- Server continues to process the request
- Client uses that handle to check for status
- Server DOES not reply until it has the response
  - The connection is still there but server only responds when ready to
- So we got a handle, we can disconnect and we are less chatty
- Some variation has timeouts too

## Pros

- less chatty
- Backend friendly - dont overwhlem it
- client can disconnect

## Cons

- not real time

## Links
- https://www.baeldung.com/spring-mvc-long-polling
