# Remote Procedure Calls

## Links

- https://www.quora.com/What-is-RPC-and-RMI
- https://www.youtube.com/watch?v=VNllljvhcnk

## GRPC

- gRPC is an open-source RPC framework that is created and used by Google. It is built upon HTTP/2.0 which makes bi-directional communication possible. gRPC communicates using binary data using protocol buffers by default for serializing structured data. gRPC servers allow cross-language unary calls or stream calls.
- RPC is a method for executing a procedure on a remote server, somewhat akin to running a program on a friend’s computer miles from your workstation.
- RPC functions upon an idea of contracts, in which the negotiation is defined and constricted by the client-server relationship rather than the architecture itself. RPC gives much of the power (and responsibility) to the client for execution, while offloading much of the handling and computation to the remote server hosting the resource.
- gRPC is usually the end system driving and facilitating communication between disparate services and APIs.

## Advantages

- gRPC can use protocol buffer for data serialization. This makes payloads faster, smaller and simpler.
- Just like REST, gRPC can be used cross-language which means that if you have written a web service in Golang, a Java written application can still use that web service, which makes gRPC web services very scalable.
- gRPC uses HTTP/2 to support highly performant and scalable API’s and makes use of binary data rather than just text which makes the communication more compact and more efficient. gRPC makes better use of HTTP/2 then REST. gRPC for example makes it possible to turn-off message compression. This might be useful if you want to send an image that is already compressed. Compressing it again just takes up more time.
- It is also type-safe. This basically means that you can’t give an apple while a banana is expected. When the server expects an integer, gRPC won’t allow you to send a string because these are two different types.
- High performance along with Safety : gRPC is high performance with google protobuf and http/2 protocol which is Multiplexed, single tcp connection , transports data as binary, enables duplex streaming etc.
- Duplex streaming : Allows clients side and service streaming simultaneously.
- First Class Load Balancing: gRPC has built in library feature it can intelligently pick which backend to send traffic to.
- Selective message compression: If you are streaming mixed text and images over a single stream (or really any mixed compressible content), you can turn off compression for the images.
- Auto generated client code: With protoc we can easily generate the client code and server code.
- Heavily optimized: gRPC library is under continuous benchmarks to ensure there are no speed regressions.
- Connection Pool : We can create connection pool containing persistent connection to server through managed channels with states connected or idle.
- RPC is very popular for IoT devices and other solutions requiring custom contracted communications for low-power devices.
- The biggest feature added by gRPC is the concept of protobufs. Protobufs are language and platform neutral systems used to serialize data, meaning that these communications can be efficiently serialized and communicated in an effective manner.
- gRPC has a very effective and powerful authentication system that utilizes SSL/TLS through Google’s token-based system

## Disadvantages

- No support for browsers hence cannot be used for external services.
- No url end points hence can’t be tested with postman or curl to check the response.
- No predefined status codes and creating custom status code may end up in conflicts.

## When to use

- When the microservices is only internal and when one server needs to talk to the other.
- When your internal services requires duplex streaming with high load of data.
- When you don’t feel to write client libraries
-
## Links

- https://medium.com/@EdgePress/is-grpc-the-future-of-client-server-communication-b112acf9f365
- https://grpc.io/docs/guides/index.html
- https://www.quora.com/What-are-the-pros-and-cons-of-REST-versus-RPC
- https://www.careerride.com/RMI-advantages-and-disadvantages-of-RPC.aspx
- https://searchapparchitecture.techtarget.com/definition/Remote-Procedure-Call-RPC
- http://www.bizcoder.com/rpc-vs-rest-is-not-in-the-url
- https://www.baeldung.com/grpc-introduction
- https://medium.com/better-programming/understanding-grpc-60737b23e79e
- https://www.freecodecamp.org/news/what-is-grpc-protocol-buffers-stream-architecture/
