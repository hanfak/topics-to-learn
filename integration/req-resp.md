# Request & Response

- Used when everything is done or asked for is within a single request-response 

## Model

- Steps
  - Client sends a Request
  - Server parses the Request
  - Server processes the Request
  - Server sends a Response
  - Client parses the Response and consume
- In general parsing and processing a request/response is considered as one step

## Parsing

- parsing aka serialization aka marhsalling/unmarshalling
  - turn some data into a format for transfer into something that can be used in code (objects), and vice versa
- The cost of parsing needs to be thought about
  - can be very expensive
    - ie xml
    - size can of payload, if you use better format (ie json) but is massive then it can be expensive
- Trade off between human readable (xml/json) but slow, vs non human readable (protbuff) but fast
- Trade off between schema for consistency and correctness vs schemaless for size and freedom,

## Uses

● Web, HTTP, DNS, SSH
● RPC (remote procedure call)
  - Leaky abstraction
● SQL and Database Protocols
● APIs (REST/SOAP/GraphQL)
● Implemented in variations

## Anatomy
- A request/response structure (the protocol) is defined and agreed by both client and server
- Request/response has a boundary
- Defined by a protocol and message format
  - format needs to be understood if it is to be used (ie json) so it can parse it

## Issues

- if sending request, there are so many places that can fail
  - ...
  - To avoid this, esp if sending a large request, can split the request payload into smaller requests with id. IF one/many fails, then the server can say they didnt get them ask to be resent. This requires extra logic on client and server to make the req/resp more reliable
    - same can apply to a response, if part is missing the client can ask the server for missing parts
- Notifications dont work well
  - client needs info from server to find out if somethign is done, or if new info to get  
  - end up doing polling, constantly call the server on schedule to check, poor scaling and extra load on server
- chat
  - high latency
  - spam server with empty requests
- Very long running requests
  - waiting a long time
  - Can end up failing, and having to restart it from scratch
  - if disconnects, then the client may not what to do
    - use of time outs
  - Blocking, have to wait for it to finish before continuing
    - Depends if wrapped in callback/future
  - better to use aysnc process
