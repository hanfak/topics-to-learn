# TCP - Transmission Control Protocol

- TCP is a utility built on top of IP
- TCP was created to solve a problem with IP
  - Data over IP is typically sent in multiple packets because each packet is fairly small (2^16 bytes).
  - Multiple packets can result in
    -  lost or dropped packets and
    - disordered packets
    - thus corrupting the transmitted data
  - TCP solves both of these by guaranteeing transmission of packets in an ordered way.
- the packet has a header called the TCP header in addition to the IP header.
  - TCP header contains information about the ordering of packets, and the number of packets and so on.
- TCP needs to establish a connection between source and destination before it transmits the packets, and it does this via a "handshake".
  - This connection itself is established using packets where the source informs the destination that it wants to open a connection, and the destination says OK, and then a connection is opened.
  -  is what happens when a server "listens" at a port - just before it starts to listen there is a handshake, and then the connection is opened (listening starts).
  - one sends the other a message that it is about to close the connection, and that ends the connection.

## links

- https://www.youtube.com/watch?v=xdQ9sgpkrX8
- https://www.youtube.com/watch?v=NdvWI6RH1eo
- How TCP Works - The Handshake: https://www.youtube.com/watch?v=HCHFX5O1IaQ
