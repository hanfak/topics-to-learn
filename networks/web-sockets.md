# Web sockets

- [Web sockets](#web-sockets)
    * [What](#what)
    * [Key features](#key-features)
    * [Where used](#where-used)
    * [Disadvantages](#disadvantages)
    * [Scaling](#scaling)
    * [When not to use](#when-not-to-use)
    * [Alternatives](#alternatives)
    * [How to implement](#how-to-implement)
    * [Links](#links)
    * [Examples Links](#examples-links)

## What 

- a communication protocol that provides full-duplex communication channels over a single TCP connection
- Defined by the WebSocket Protocol. It is a standardized protocol that defines the rules and format for establishing and maintaining a WebSocket connection between a client and a server.
  - RFC 6455 https://www.rfc-editor.org/rfc/rfc6455
  - operates at the application layer of the TCP/IP stack and is independent of the underlying transport protocol. 
  - It uses the standard WebSocket URI scheme, which is 
    - "ws://" for unencrypted connections and 
    - "wss://" for encrypted connections (WebSocket Secure)
  - Contains two main parts 
    - Handshake:
      - the initial step to establish a WebSocket connection. 
      - It follows the HTTP protocol to upgrade the connection from HTTP to the WebSocket Protocol. 
      - The client sends a special HTTP request to the server, known as the WebSocket handshake request, indicating its desire to switch protocols.
      - The server responds with an HTTP 101 status code (Switching Protocols) if it supports WebSockets, indicating a successful upgrade to the WebSocket Protocol.
    - Data Framing: 
      - Once the WebSocket connection is established, data is exchanged in the form of messages between the client and the server. 
      - The WebSocket Protocol defines a framing mechanism to encapsulate and format these messages for transmission. 
      - The framing includes a header that specifies the message type (text or binary) and the length of the payload. 
  - Other features include
    - message fragmentation
    - ping-pong heartbeats for connection monitoring
    - extensions for additional functionality like compression or security
- supported by most modern web browsers

## Key features 
- Persistent Connection: 
  - maintain a long-lived connection between the client and the server, allowing for real-time communication.
- Full-Duplex Communication
  - enable simultaneous communication in both directions.
  - The client can send messages to the server, and the server can push data to the client without waiting for a request.
- Lightweight Overhead
  - a smaller overhead compared to traditional HTTP connections.
  - The initial handshake is slightly larger, but subsequent messages have minimal framing overhead.
  
  
## Where used 
- Chat Applications
  - ideal for building chat applications where multiple users need to exchange messages in real-time. 
  - With WebSockets, messages can be instantly sent and received, enabling seamless communication between users.
- Real-Time Collaboration
  - WebSockets are well-suited for collaborative applications such as 
    - collaborative document editing
    - project management tools
    - whiteboard applications
  - WebSockets enable real-time updates and synchronization of changes across multiple clients.
- Live Dashboards
  - display real-time data and updates, such as 
    - monitoring systems
    - financial tickers
    - analytics dashboards
  - The server can push updates to connected clients without clients needing to constantly poll the server.
- Multiplayer Games
  - allowing players to interact with each other in real-time
  - enable quick and efficient communication between players and the game server, facilitating real-time gameplay and synchronization.
- Stock Market or Auction Applications
  - provide real-time updates and notifications in stock market applications or online auction platforms. 
  - Users can receive instant updates on stock prices, bids, or auction status changes without manually refreshing the page.
- Notification Systems
  - where clients need to be notified instantly about new events, messages, or updates
  - social networks, messaging apps, or any application that requires real-time notifications
- IoT (Internet of Things)
  - establish a real-time connection between IoT devices and a central server
  - enables devices to send sensor data, receive commands, and provide real-time updates to control systems or user interfaces.

## Disadvantages 

- Complexity
  - can be more complex compared to traditional HTTP connections. WebSocket implementation requires additional server-side and client-side code, as well as handling various events and message protocols. 
  - This complexity can increase development time and may require a deeper understanding of the WebSocket protocol.
- Server Resources
  - maintain a persistent connection between the client and the server, which can consume server resources. 
  - Each open WebSocket connection requires a certain amount of memory and processing power on the server side. Handling a large number of concurrent WebSocket connections can put a strain on server resources and require careful management to avoid performance issues.
- Proxy and Firewall Compatibility
  - Some proxies and firewalls are not WebSocket-aware or may not support the WebSocket protocol.
  - This can cause connectivity issues if WebSocket traffic is blocked or improperly handled by intermediate network devices. 
  - To ensure WebSocket connectivity, it may be necessary to configure or bypass certain network infrastructure components.
- Limited Browser Support
  - While modern web browsers widely support WebSockets, some older or less common browsers may lack WebSocket support or have incomplete implementations. If you need to support a wide range of browsers, you may need to consider fallback mechanisms or alternative communication methods for clients that don't support WebSockets.
- Scalability
  - Scaling WebSocket applications to handle a large number of concurrent connections can be challenging. 
  - As the number of active WebSocket connections increases, the server needs to efficiently manage resources and handle the increased load.
  - Load balancing and horizontal scaling strategies may be required to handle high traffic volumes.
- Stateful Connections
  - WebSockets maintain a stateful connection between the client and the server. 
  - This means that the server needs to keep track of the connection state and associated data for each WebSocket client. 
  - Managing and synchronizing this state can introduce complexities, especially in distributed or clustered server environments.
  - 

## Scaling 

- involves ensuring that your application can handle a large number of concurrent connections and deliver real-time updates efficiently.
- Optimize resource utilization: Make sure your server efficiently manages resources (such as memory and CPU) for WebSocket connections.
- Consider using lightweight data structures, connection pooling, and efficient event-driven programming models.
- Set appropriate limits on the number of concurrent WebSocket connections your server can handle. 
  - prevent resource exhaustion and ensures fair resource allocation.
- Distribute incoming WebSocket connections across multiple servers using a load balancer. 
  - This enables horizontal scaling and distributes the load evenly among backend servers
- Vertical scaling: Upgrade your server hardware by adding more powerful CPUs, increasing memory, or utilizing faster network interfaces
- Horizontal scaling:
  - Add more servers to your WebSocket application by using techniques like server clusters or distributed systems. 
  - Each server handles a subset of WebSocket connections, and load balancing distributes connections across multiple servers.
- Caching for frequently accessed data
- Pub/Sub Systems 
- Optimize message processing: 
  - Minimize the processing required for each message by offloading heavy computations or non-real-time tasks to background processes or worker threads. 
  - Prioritize message processing based on importance or timestamp to ensure timely delivery of critical updates
  - Compress WebSocket messages to reduce network bandwidth usage, especially for large payloads.
    - Consider optimizing the size of transmitted data to minimize latency and improve overall performance.
- Implement monitoring tools and collect metrics to understand the performance and health of your WebSocket infrastructure. 
  - Monitor connection counts, server load, latency, and other relevant metrics to identify bottlenecks and make data-driven scaling decisions.
- Utilize auto-scaling mechanisms provided by cloud platforms to automatically scale your WebSocket infrastructure based on predefined thresholds or metrics to handle varying loads

## When not to use

- application primarily involves simple request-response interactions without the need for real-time updates or continuous communication, using regular HTTP requests may be sufficient
- Low Latency, High Frequency Data Transfer
  - more specialized protocols or technologies, such as UDP-based solutions or custom networking frameworks should be used
- Limited Server Resources
  - maintain open connections between clients and servers, which can consume server resources
  - alternatives like long polling or server-sent events that allow for more efficient resource utilization
- Compatibility Requirements
  - Older technologies may not be able to use this protocol
- can introduce security considerations, particularly when it comes to cross-origin resource sharing (CORS) and authentication
  - 

## Alternatives

- Long Polling
  - a technique where the client sends a request to the server and keeps the connection open until the server has new data to send or a timeout occurs. 
  - When new data is available, the server responds to the client, and the client immediately sends a new request to maintain the connection. 
  - Long polling can simulate real-time communication effectively but requires more server resources and incurs additional latency compared to WebSockets
- Server-Sent Events (SSE)
  - unidirectional communication protocol that allows the server to push data to the client over a single HTTP connection. 
  - provides a simple API for the server to send data as events, which the client can receive and process. 
  - suitable for scenarios where only server-to-client communication is required, without the need for bidirectional communication.
- Comet is a technique that enables server-to-client pushing of data over HTTP. 
  - uses techniques like long polling, hidden iframes, or streaming to establish a persistent connection between the client and server. 
  - Comet is a generic term that encompasses various approaches to achieving real-time communication over HTTP, including long polling and streaming.
- WebRTC (Web Real-Time Communication)
  - set of APIs and protocols that enable real-time communication between web browsers
  - provides peer-to-peer audio, video, and data streaming capabilities without the need for server intermediation
- GraphQL Subscriptions
  - allows clients to subscribe to specific data changes on the server.
  - the server can push updates to clients when the subscribed data changes. While GraphQL subscriptions are primarily focused on data updates, they can be used for real-time communication in certain scenarios.
  
## How to implement

- Two sides server and client implementations 
- Server-Side Implementation
  - Genearlly use a library/framework to handle this 
  - Set up a WebSocket server
    - creating a WebSocket server object, specifying the desired routes or endpoints
    - defining the logic for handling incoming WebSocket connections and messages.
  - Implement the logic to handle WebSocket events (Event handlers) such as
    - connection establishment
    - message reception
    - errors
    - disconnection
  - Implement the functionality to broadcast messages to all connected clients or send targeted messages to specific clients.
    - This involves keeping track of connected WebSocket clients and sending messages to the appropriate recipients. 
- Client side implementation
  - Create a WebSocket object in your client-side code and establish a connection to the WebSocket server.
    - Provide the appropriate WebSocket server URL or endpoint.
  - Define event handlers for WebSocket events such as connection open, message received, error, and connection close. 
    - These event handlers will handle the server's responses and allow your client-side code to react accordingly.
  - Implement the code to send messages from the client to the server using the WebSocket object's send() method. Same for receive
  - Implement the functionality to close the WebSocket connection when it's no longer needed

## Links 

- https://www.youtube.com/watch?v=2Nt-ZrNP22A
- https://www.html5rocks.com/tutorials/websockets/basics/
-  http://cometdaily.com/2008/07/04/html5-websocket/
- https://ably.com/topic/websockets
- https://ably.com/blog/websockets-vs-long-polling
WebSockets are a thin transport layer built on top of a device’s TCP/IP stack. The intent is to provide what is essentially an as-close-to-raw-as-possible TCP communication layer to web application developers while adding a few abstractions to eliminate certain friction that would otherwise exist concerning the way the web works
- https://www.youtube.com/watch?v=8ARodQ4Wlf4
- https://www.youtube.com/watch?v=2Nt-ZrNP22A

## Examples Links 

- https://www.youtube.com/watch?v=U4lqTmFmbAM java spring
