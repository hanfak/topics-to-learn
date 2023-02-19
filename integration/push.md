# Push

- I want it as soon as possible
- A different model to request/response
  - instead of constant asking for the info, and getting nothing back (waste of resources)
  - The server will give the information back to the client when it is ready

## How it works

- Client connects to a server
- Server sends data to the client
- Client doesn’t have to request anything
- Protocol must be bidirectional
  - websockets is bidirectional

## Uses

- real time notification
- chat
- rabbitmq
  - producers/senders and listeners are connected to the broker using push
  -

## pros

- real time, dont wait for notification

## Issues

- Push infers forcing
- The client might not be able to handle the number of pushes from the server
  - notifications might get lost/dropped
- Long running connections
  - can drop
  - client must always be online
- if lots of clients are linked to a server for the same notification, it takes up too much resources
- requires bidirectional connection
  -
