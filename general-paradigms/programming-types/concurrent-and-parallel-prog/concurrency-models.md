# Concurrency Models

- specifies how threads in the the system collaborate to complete the tasks they are are given

## shared state concurrency mode
- multiple threads executing within the same application would also share objects.
- causes a lot of concurrency problems which can be hard to solve elegantly.

## shared nothing or shared nothing
- the threads do not share any objects or data. This avoids a lot of the concurrent access problems of the shared state concurrency model.
- asynchronous "separate state" platforms and toolkits like Netty, Vert.x and Play / Akka
