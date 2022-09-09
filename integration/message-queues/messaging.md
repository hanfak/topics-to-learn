# Messaging

- Use of asychronous processing
- instead of telling the system what to do step by step, we break down the work into smaller pieces and let it decide the optimal execution order.
  - As a result, things become much more dynamic, but also more unpredictable
- Helps to scale applications and increase fault tolerance

## Uses

- Decouple producers and consumers, asynchronous processing
  - consumer does not need to be up for message to be processed
- Improve reliable communication
  - req resp via two message queues
- Can increase scalability
  - Add more replica consumers to a queue
- Buffer in front of services
  - Prevent overloading a service
  - reduce timeouts
- A means of retry an event
  - if an event fails, it can send the message back to the same queue it retrieved the message and reprocess again later
  - Based on a cron job, can consumer a messsage at a specificed time 
- Can parallelise requests
  - pub sub same messages can be handled by multiple (same or different consumers)
  - queue - multiple different messages can be handled by different consumers
- Can place errored messages on a dead letter queue which can handled separately
- For long running processes, background jobs, batch jobs
- when you dont need to cater for immediate responses or need to be part of a basic transaction

## Use cases

- https://stackify.com/message-queues-12-reasons/
- https://www.quora.com/What-are-some-use-cases-for-message-queues-in-real-life-and-what-are-some-architectures-that-achieve-the-same-goal-without-using-queues-explicitly
- https://blog.iron.io/top-10-uses-for-message-queue/

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
