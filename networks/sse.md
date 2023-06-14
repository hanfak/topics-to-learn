# Server sent events (SSE)

## What
- server-side technology that enables real-time, push-based communication from a server to a client over a single HTTP connection
- allows the server to send continuous updates or event streams to the client without the need for the client to continuously poll or make repeated requests.

## Key features 

## Advantages 

Server-Sent Events (SSE) offer several advantages for real-time communication between a server and a client.
- Simplicity
  - SSE is relatively simple to implement and understand compared to other real-time communication technologies like WebSockets. 
  - It uses standard HTTP connections and can be handled using standard web server frameworks. The server-side code for sending events is straightforward, making it accessible to developers with basic web development knowledge. 
- Compatibility
  - SSE works over standard HTTP connections, making it compatible with existing web infrastructure and widely supported by web servers and frameworks. 
  - supported by most modern web browsers without requiring additional plugins or libraries, allowing for broad client compatibility.
- Real-time Updates
  - enables real-time updates and event-driven communication from the server to the client
  - allows the server to push data or event notifications to the client as soon as they are available, eliminating the need for the client to poll the server repeatedly
  - This real-time communication capability is useful for applications that require instant updates, such as live feeds, notifications, or collaborative applications.
- Improved Efficiency
  - uses a persistent HTTP connection between the client and the server. 
  - eliminates the overhead of establishing new connections for each update and reduces the amount of network traffic compared to traditional polling techniques. 
  - allows for efficient, low-latency data delivery while minimizing unnecessary requests and reducing server load.
- Automatic Reconnection
  - includes automatic reconnection mechanisms. 
  - If the connection between the client and the server is interrupted due to network issues or server restarts, the client will automatically attempt to reconnect to the server and resume the event stream. 
  - ensures the continuity of the real-time updates and improves the reliability of the communication.
- Event Metadata
  - allows the server to include metadata along with each event, providing additional information about the event, such as an event identifier or timestamp. 
  - This metadata can be used by the client to process and handle events differently based on their types or properties.
- Progressive Enhancement
  - can be used as a progressive enhancement technique.
  - can be added to an existing web application without requiring major changes to the application's architecture.
  - can be selectively enabled for browsers that support it, while falling back to other techniques like polling or long-polling for browsers that do not support SSE.

These advantages make Server-Sent Events a viable choice for applications that require real-time updates or event-driven communication from the server to the client. 


## Examples

## Disadvantages/ when not to use

## Alternatives 
Unidirectional Communication: SSE provides a unidirectional communication channel where the server can send data or events to the client. The client, however, cannot send data back to the server using SSE. It is primarily used for server-to-client data push.

Persistent Connection: SSE establishes a long-lived HTTP connection between the client and the server. This connection remains open for an extended period, allowing the server to send updates to the client whenever new data or events are available.

Event Streams: The server sends data to the client as a stream of events. Each event consists of a text payload and optional metadata, such as an event name or identifier. Clients can handle different events based on their types and process the associated data accordingly.

Automatic Reconnection: SSE includes automatic reconnection mechanisms. If the connection between the client and the server is interrupted, the client will automatically attempt to reconnect to the server, ensuring the continuity of the event stream.

Simple Integration: SSE is relatively easy to implement and integrate into web applications. It uses standard HTTP protocols and can be supported by web servers and frameworks that provide SSE functionality.

## Links 
- https://codeburst.io/polling-vs-sse-vs-websocket-how-to-choose-the-right-one-1859e4e13bd9
