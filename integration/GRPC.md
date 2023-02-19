# GRPC

- Google Remote Procedural Call
- framework for implementing RPC APIs via HTTP/2
- Uses a compact schema for data
  - compile to different languages
- Takes advantage of HTTP2
- similar to other rpc protocols which have a shared schema like cobra

## Why

- There are many protocols out there
- For every protocol you need to build a client library to communicate
  - this is hard to update
- REST has a lot of hidden meta data so not as lightweight
- In Grpc everything is hidden,

## Uses

- Unary RPC
  - request response
- Server streaming RPC
  - server side streaming
  - ie logging, progress of job, retrieving a large file
- Client streaming RPC
  - sending a large file to the server
- Bidirectional streaming RPC
  - chat
- inter microservice communication
  - multi language apps communicating
- For internal APIs where you don’t have to force technology choices on clients
- When efficient communication is a goal
- Real-time communication services where you deal with streaming calls

## Pros

- fast and compact
  - messages smaller than json
- one client library
  - consistent usage
  - Has many features
- Cancel a http2 request
- TLS needs to be used
- Has automated code generation from the schema

## Issues
- Stuck to http2
- Uses binary format (protobuff)
  - hard to inspect, not readable
  - auditing needs to be done before conversion
  - To analyze payloads, perform debugging, and write manual requests, devs must use extra tools like gRPC command line tool and server reflection protocol.
- Thick client
  - does a lot
  - reliant on it, can have bugs
- hard to integrate a proxy
- No native browser support
- Lack of maturity
  - minimal support about best practices, workarounds, and success stories
- Steeper learning curve
- similar to other rpc protocols which have a shared schema
  - everyone is tied to the schema, if one changes then everyone else has to change
  -  It requires tight coupling between client and server
-  It uses non standard naming and discovery which doesn't work across network boundaries, which is why SOAP and XML-RPC were invented, a way of channelling RPC over port 80/443.
-  The lack of standards for caching of responses or middleware boxes for load balancing, rate limiting, deployment practices.
- Trying to "wish away" the network by abstracting it out of existence
- It doesn't solve the problem that RPC leaves the definition of the verbs (ie the procedures) and how they modify state of a common thing undefined. If I call an RP twice, what is the effect? How do I know it succeeded? What happens if it fails? etc etc

## Protocol buffers

- structuring messages developed and used in inter-machine communication

### How

- In a .proto text file, a schema is defined
  - how they want data to be structured
  - use numbers, not field names, to save storage
  - They can also embed documentation in the schema.
- Use a protoc compiler
  - this file is then automatically compiled into any of the numerous supported languages
- At runtime, messages are compressed and serialized in binary format

## Advantages

- efficient parsing
  - Less CPU-intensive because data is represented in a binary format which minimizes the size of encoded messages
  -  message exchange happens faster, even in devices with a slower CPU like IoT or mobile devices
- Schema is essential
  - ensure that the message doesn’t get lost between applications
  - its structural components stay intact on another service as well

## Use of http2

- communication is divided into smaller messages and framed in binary format
  - messages compact and efficient
- Multiple parallel requests
  - supports multiple calls via the same channel
  - communication is bidirectional — a single connection can send both requests and responses at the same time
- Streaming
  - Real time communication
  -  each stream is divided into frames that can be prioritized and run via a single TCP connection, thus reducing the network utilization and processing load
