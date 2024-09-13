# Messaging

- Use of asychronous processing
- instead of telling the system what to do step by step, we break down the work into smaller pieces and let it decide the optimal execution order.
  - As a result, things become much more dynamic, but also more unpredictable
- Helps to scale applications and increase fault tolerance

## Uses

- Decouple producers and consumers, asynchronous processing
  - consumer does not need to be up for message to be processed
  - Can handle failures of consumer, or removing a consumer (For upgrade)
- Improve reliable communication
  - req resp via two message queues
  - can store messages that has not been consumed on the queue, in case of queue failure
- Can increase scalability
  - Add more replica consumers to a queue to handle increased load
- Buffer in front of services
  - Prevent overloading a service
  - reduce timeouts
- Ordering of tasks
  - Dependent on implementation
    - ie guarantees ordering from one producer to a queue and if single consumer is used
- A means of retry an event
  - if an event fails, it can send the message back to the same queue it retrieved the message and reprocess again later
  - Based on a cron job, can consumer a messsage at a specificed time 
- Can parallelise requests
  - pub sub same messages can be handled by multiple (same or different consumers)
  - queue - multiple different messages can be handled by different consumers
- Can place errored messages on a dead letter queue which can handled separately
  - Can also resend a message to another queue to replayed with max retry
- For long running processes, background jobs, batch jobs
- when you dont need to cater for immediate responses or need to be part of a basic transaction
- Delay processing of a task
- separate tasks that can fail and can be retryable
- have “timeout errors” due to too many requests at the same time
- polling a data store too often and you want this data store to be available to answer qualified queries instead
- Notify consumers of events
- architectural reasons
  -  Decoupling
  -  Redundancy
  -  Scalability
  -  Elasticity & Spikability
  -  Resiliency
  -  Delivery Guarantees
  -  Ordering Guarantees
  -  Buffering
  -  Understanding Data Flow
  -  Asynchronous Communication


## Examples 
- Image processing
- Database backup 
- Email communication
- Performing large computations and tasks across a network of servers
- Updating the status of files
- Sending real-time data to other services and programs
- Payments

## Use cases

- https://stackify.com/message-queues-12-reasons/
- https://www.quora.com/What-are-some-use-cases-for-message-queues-in-real-life-and-what-are-some-architectures-that-achieve-the-same-goal-without-using-queues-explicitly
- https://blog.iron.io/top-10-uses-for-message-queue/
- 

## Drawbacks

- https://www.programmableweb.com/news/why-messaging-queues-suck/analysis/2017/02/13
- https://techblog.bozho.net/you-probably-dont-need-a-message-queue/
- https://www.reddit.com/r/programming/comments/arjaee/counter_arguments_to_using_message_queuesbrokers/



## Links

- https://www.youtube.com/watch?v=sjDnqrnnYNM
- https://www.youtube.com/watch?v=Yz8HXTFMqcE&list=WL&index=4&t=0s
- https://www.freecodecamp.org/news/rabbitmq-9e8f78194993/
- https://examples.javacodegeeks.com/rabbitmq-tutorial-for-beginners/
- https://www.youtube.com/watch?v=DXTHb9TqJOs
