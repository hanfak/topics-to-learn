# Streaming

## What

- Streaming solves the constant polling problem.  If constantly hitting the server is necessary, then it's better to use something called web-sockets.
- Websockets
  - is a network communication protocol that is designed to work over TCP. It opens a two-way dedicated channel (socket) between a client and server, kind of like an open hotline between two endpoints.
  - Unlike the usual TCP/IP communication, these sockets are "long-lived" so that its a single request to the server that opens up this hotline for the two-way transfer of data, rather than multiple separate requests.
    - By long-lived, we meant that the socket connection between the machines will last until either side closes it, or the network drops.
  - Web-sockets mean that there is a single request-response interaction and that opens up the channel through which two-data is sent in a "stream".
- The big difference with polling and all "regular" IP based communication is that whereas polling has the client making requests to the server for data at regular intervals ("pulling" data), in streaming, the client is "on standby" waiting for the server to "push" some data its way
  - The server will send out data when it changes, and the client is always listening for that
  -  if the data change is constant, then it becomes a "stream", which may be better for what the user needs.
- For example, while using collaborative coding IDEs, when either user types something, it can show up on the other, and this is done via web-sockets because you want to have real-time collaboration.  Thus avoid lag
- For example
  - multiplayer games
  - Chat rooms

## example

- Kafka

## when

-  you want to stream if your data is "real-time",
