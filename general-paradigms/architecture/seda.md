# stage event driven architecture (SEDA)

- approach to software architecture that decomposes a complex, event-driven application into a set of stages connected by queues.
- It avoids the high overhead associated with thread-based concurrency models (i.e. locking, unlocking, and polling for locks), and decouples event and thread scheduling from application logic.
- By performing admission control on each event queue, the service can be well-conditioned to load, preventing resources from being overcommitted when demand exceeds service capacity.
- SEDA employs dynamic control to automatically tune runtime parameters (such as the scheduling parameters of each stage) as well as to manage load (like performing adaptive load shedding).

### Examples 
- E-commerce websites:
  - often have to handle large volumes of traffic, so it's important for them to be scalable. 
  - when a customer places an order, the order information can be placed in an event queue. A worker thread then polls the event queue for new orders, and processes each order in turn. This allows the e-commerce website to handle a large number of orders without becoming overloaded.
- Social media platforms: 
  - handle large volumes of traffic.
  -  when a user posts a new message, the message can be placed in an event queue. A worker thread then polls the event queue for new messages, and processes each message in turn.
- Streaming media services
  - need to be able to deliver high-quality video and audio to users, even when there is a lot of traffic. 

### when not to use

- Real-time processing: not well-suited for real-time applications, because it can introduce latency. 
- Low latency:  can introduce latency, which can be a problem for applications that require low latency. 
- Simple applications:  is overkill for simple applications. For simple applications, a simpler architecture, such as a request-response architecture, may be a better choice.
## Benefits 
- Scalability: scalable architecture that can be easily scaled up or down to meet demand. 
- Performance: improve performance by decoupling event and thread scheduling from application logic. 
- Reliability: improve reliability by performing admission control on each event queue. 
- Modularity: easily decomposed into a set of modules, which makes it easier to develop, test, and deploy.
## Drawbacks 
- Complexity: complex architecture to implement and manage. 
- Cost: more expensive to implement than other architectures. 
- Learning curve: steep learning curve, which can make it difficult to get started.
### Causes low latency 
- Oversubscription occurs when there are more messages in the queue than there are worker threads to process them. This can lead to long delays as messages wait to be processed.
  - Fix 
    - Use the right number of worker threads: The number of worker threads should be equal to or greater than the number of messages in the queue. This will ensure that no messages are waiting to be processed.
- If the processing time for each event is too long, it can cause high latency. This can be caused by a number of factors, such as complex logic, slow database queries, or network latency.
  - Fix 
    - The processing time for each event should be as short as possible. This can be done by using efficient algorithms, caching data, and using a load balancer.
- If the queue management is not efficient, it can lead to high latency. This can be caused by factors such as using a single queue for all events, not using a load balancer, or not using a queue management tool.
  - fix 
    - A load balancer can help to distribute the load evenly across multiple worker threads. This can help to reduce latency by preventing any one worker thread from becoming overloaded.
- Network latency can cause high latency if the messages have to travel a long distance to be processed. This is especially true for applications that are distributed across multiple regions or countries.
  - Fix 
    -  try to reduce network latency by using a local queue or by moving the application closer to the users.
    