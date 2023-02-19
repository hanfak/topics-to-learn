# Publish Subscribe

- One publisher many readers

## How
- Client publishes something/message to a server and moves on, does not need to wait for it to be processed
  - This publisher does not know who picks it up, just that it will be picked up by those interested in it
- Another client can register with the server and listen for a specific message and consume it
  - The reader/subscriber only knows there is a message that it wants and reads/consumes it
    - Depending on settings it will tell the server/broker when it has consumed it so it can be removed from the server  
      - this is known as a queue
  - Does not know who it came from
  - Done via long polling or push
- The server is often called the broker, it does not process the message, just receives and sends it on
- Generally, the message removed from the server when all the readers/subscribers have received the message
  - Settings can be set to not remove and keep for a set time -> so new subscribers can get this message


## Why

- Lots of chatty applications, Especially for sending the same request to multiple servers
- Due to lots of failures that can occur in req/resp using an intermediary (broker) reduced chattiness, lost messages etc
- Decoupled the sender and receiver
- Fire and forget mechanism allows for aysnc processing, the client does not have to wait for long processing of their request, the processing can be done in the background and take it's time (within reason)
  - if it needs information back, it can subscribe to another topic/queue/channel (Where the messages are published) to get it back at a later date
- If there were lots of calls from one server to another, then req/resp will block waiting, lots of chnace of failure between communication downstream which will break the whole flow
- Scale with multiple consumers/subscribers
  - if lots of unique messages need to be processed add more consumers
  - if one message needs to be handled in different independent ways can split the processing into different message consumers within an app or as separate applications (microserves)
- Your client does not have to be running and your message will be processed
  - as long as it was sent to the broker
- Your server can be down, but it will be processed
  - if on a queue it will sit there (although the queue can overfill if the publish keeps adding)
  - same for multiple subscribers if there was a time to live for the message

## Issues

- Two general problem
  - How do i know the message was delivered
- Different guarantees
  - At least once guarantee - the message can be consumed by a subscriber twice, so adds complexity to handle this
    - ie idempotent, immutable
- Added complexity
  - especially with handling sad paths, how to rollback
- Another thing to maintain
- The broker is point of failure
  - Can have persistent store, but slows performance
- Harder to debug
  - need tracing, correlation id, message id
  - How to flow the full flow for a single starting message
