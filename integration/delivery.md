# Delivery

- Delivery of messages/requests in distributed systems
- we can’t deliver messages reliably and in order in the face of network partitions and crashes without a high degree of coordination. This coordination, of course, comes at a cost (latency and availability), while still relying on at-least-once semantics.

## at-most-once delivery

## at-least-once delivery

- at-least-once delivery is also impossible because, technically speaking, network partitions are not strictly time-bound.
   - If the connection from you to the server is interrupted indefinitely, you can’t deliver anything.
## Exactly once delivery

- impossible
  - See the two generals problem
- https://bravenewgeek.com/you-cannot-have-exactly-once-delivery/
