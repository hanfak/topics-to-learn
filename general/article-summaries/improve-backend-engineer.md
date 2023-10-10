# How to Become a Good Backend Engineer (Fundamentals)

- one thing always remain constant; The first principals the tech is built on
- the fundamental infrastructure on which the tools, frameworks or languages are built rarely does.
- FOCUS ON THE FUNDAMENTALS THAT EVERYTHING IS BUILT UPON
  - They rarely change
  - Always useful
  - Can understand and use new tech easier from these
- There are two paths
  - to have basic understanding of all these fundamentals and become a jack-of-all-trades backend engineer 
  - or go vertical in one at deeper level and become expert in that area. T- shaped
- become a better backend engineer is never clean
  - it is full of trial and errors and experimentations that only you have to experience
  - best way is to get your hands dirty.
- There are reasons for everything
- The key:
  - know how a something works and what is the strength and weaknesses you will know when to use it.
- it is important to explore different technologies to find what interests you and where your strengths are
- As you gain more experience and expertise, focus on deepening your knowledge in a specific area to become known for your skill in that field.
- nothing is written in stone, you can change anything.
- Areas

## Communication Protocols
- Communications protocols link the frontend to the backend, or different services within the backend
- Understanding how protocols work 
- either built on top of TCP or UDP.
  - TCP is a stream-based connection-oriented protocol while UDP is a message based and connectionless.
  - TCP provides reliable delivery at a cost of connection setup and retransmission. While UDP starts faster but doesn’t have guaranteed delivery.
- Moving up the stack, the HTTP protocol was originally built on top of TCP because we wanted to send requests and responses reliably
  - resources become richer, one connection was not sufficient to concurrently send multiple requests. So browsers started to establish more and more connections, the cost of connection setup for each request became so high.
  - HTTP/2 introduced application level streams so multiple requests can be sent on the same connection
  - Later HTTP/2 evolved and had to be rewritten on top of UDP with HTTP/3 to solve the TCP head of line problem
- using any protocol comes with a cost especially while building APIs.
  - need to understand to make informed decision to match needs
  - ie  using HTTP/2 might give you more HTTP request throughput, but the work the application needs to do to assemble the streams taxes the CPU
- real-time Bidirectional communication protocols to build chatting, gaming apps or just communicating between two services. 
  - Protocols such as WebSockets, gRPC or just raw TCP/UDP can be used. 

## Web servers 

- Web servers deliver static or dynamic content served on top of the HTTP protocol. If you build a Web API you may spin up your own web server in your language
- Configuring your web server with the appropriate protocol is critical for performance and resilience 
- Do you expect multiple concurrent requests from the same client? or do you expect fewer requests but from many clients?
- Web servers can be single or multithreaded. They can have one thread or multiple listener threads. There are many ways client connections can be accepted and distributed among the threads
- If you choose an off-the-shelf web server you are stuck with its architecture.
- If you build your own from scratch you get to choose the architecture that is right for you.
- web servers can set any where in the stack.
  - CDN, API gateways, load balancers etc

## Database Engineering

- At its core the idea of a database is simple; Allow multiple users to store and retreive data consistently and in a durable fashion.
- understanding the four properties of ACID: atomicity, consistency, isolation, and durability is necessary
  - These are not all necessary to build solutions 
  - relational databases are fully ACID and require a schema
  - MongoDB was built as a document based database, with basic atomicity (document level) and no schema.
  - Redis built a fanstatic high performance cache by sacrificing durability by default.
- indexes and at their core B+Trees is the data structure of choice
- How data is organized in tables, documents or graphs all end up as file system pages 
  - Understanding how to get most of your disk I/O read is the core of database engineering.

## Proxies

- is it receives requests from a client and forward the requests to backend servers. 
- hides the network layer identity of the original client from the destination server.
- two levels of proxying: layer 4 and layer 7 proxying.
  - Layer 4 proxying works at the transport layer
  - layer 7 proxying works at the application level
  - Layer 7 proxying require the proxy to understand the application protocol while layer 4 proxying works with any application protocol because it works at the transport layer (TCP or UDP).
- Both the forward proxy and the reverse proxy, receive requests from clients and forward the request to a backend
  - forward proxy, the client explicitly asks for a particular backend server and the proxy fulfills this request
  - Forward proxies must be configured in the client network proxy section for them to work
  - reverse proxy the client doesn’t know the final backend server, to the client the final destination is the reverse proxy.
- uses cases of proxies are caching, API gateways, authentication, load balancing 

## Messaging Systems

- important as we move towards interconnected systems and services
- As services start to communicate to each other, coupling and dependencies increase which increases the complexity of building scalable backend applications.
- designed to remove this coupling
- support a feature called publish-subscribe where a client can publish a message and other clients can subscribe to consume this content.
- Kafka use long-polling model while RabbitMQ uses push model, 
- How do you make sure the consumer reads the message only once? These guarantees complicates the messaging system design.

## Message Formats

- describe in-wire format of the message being sent. They usually broken down into two types human readable and non-human readable.
  - Examples are XML, JSON and protocol buffers.
- When a client sends a message to a backend, it needs to serialize the message from the language data structure to the on-wire message format. When the backend receives the message it needs to then deserialize the message from this format to the language data structure.
- Allows for different tech used in the commuicating apps to talk with each other
- XML was one of the original message formats designed to be human-readable. However, computers had difficulty dealing with XMLs, so protocol buffers format was created to make the message format smaller and more friendly. 
- Protocol buffers became very popular and were designed to solve the problem of high bandwidth messages. Protocol buffers minimize the payload so fewer bytes can be sent. It also speeds up the serialization and deserialization process. 

# Security

- You can secure communications with encryption or TLS. You can prevent network intrusion with firewall rules and proper network configuration. 
- You can study common software vulnerabilities and protect against denial of service attacks.
- be familiar with the different types of security risks and how to mitigate them.
- man-in-the-middle attack. This is where an attacker intercepts communication between two parties and tries to eavesdrop or modify the data being exchanged. To prevent this type of attack, it is important to encrypt and authenticate the communicated parties using Transport Layer Security (TLS).
- denial of service attack. This is where an attacker tries to prevent legitimate users from accessing a service by flooding it with requests or through finding a way to crash the backend by sending a special payload. To prevent this type of attack, it is important to have a firewall or a layer 7 DDOS protection layer in place to block illegitimate requests
- here is a client side security attacks such as XSS (cross side scripting), there are server side security attacks such as SQL injection.