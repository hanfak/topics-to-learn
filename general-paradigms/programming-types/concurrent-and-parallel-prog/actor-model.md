# Actor Model 

## What 

- A concurrency model
  - In this model, concurrency is achieved by using multiple threads of execution. Each thread represents an independent flow of control that can execute code concurrently with other threads.
- provides a high-level abstraction that simplifies the design and implementation of concurrent systems.
  - provides a declarative and message-driven approach to concurrency,
- computation is based on the concept of actors, which are independent entities that encapsulate state, behavior, and communication. Each actor is an autonomous unit of computation that can process messages asynchronously and interact with other actors through message passing.
- key principles of the Actor model:
  - Actors: 
    - Actors are the fundamental building blocks in the model. Each actor has its own internal state, behavior, and a mailbox for receiving messages. Actors are autonomous and can execute their behavior independently. They do not share mutable state with other actors, providing a clear boundary for encapsulation. 
  - Message Passing:
    - Communication between actors is achieved through message passing. Actors can send messages to other actors, which are added to the recipient's mailbox. Messages are processed sequentially by the receiving actor. Message passing is asynchronous, meaning that actors can continue processing other messages while waiting for a response.
  - Asynchronous Execution: 
    - Actors process messages asynchronously, allowing for concurrent execution. Each actor executes its behavior independently, making it possible to achieve parallelism and efficient utilization of resources. Actors can process messages in a non-blocking manner, enabling high responsiveness and scalability. 
  - Encapsulation: 
    - Actors encapsulate their state and behavior, allowing for modular and independent components. Each actor is responsible for managing its own state, and other actors can only interact with it through message passing. This encapsulation simplifies reasoning about and managing the concurrency of the system. 
  - Addressability:
    - Actors are uniquely addressable entities. Messages are sent to a specific actor's address, allowing for precise targeting and communication between actors. Actors can have local or remote addresses, enabling distributed computation across different machines or nodes.
  - Supervision: 
    - Actors can supervise other actors, defining how to handle failures and errors. Supervisors can monitor the lifecycle of actors and take appropriate actions in case of failures. This fault-tolerance mechanism allows for the creation of robust and resilient systems.

## Implementations 

Akka: Akka is a widely-used open-source toolkit and runtime for building highly concurrent, distributed, and fault-tolerant applications based on the Actor model. It provides a comprehensive set of features and abstractions for building actor-based systems, including message passing, supervision, clustering, and more.

Vert.x: Vert.x is a lightweight, event-driven, and non-blocking toolkit for building reactive applications. It offers an implementation of the Actor model through its event bus, allowing actors to communicate by sending and receiving messages over the bus. Vert.x provides other features like concurrency, scalability, and asynchronous I/O.

Reactors: Reactors is a lightweight, high-performance library for building reactive systems using the Actor model. It provides a simple and intuitive API for defining actors, sending and receiving messages, and managing concurrency. Reactors focuses on performance and low-latency messaging.

Kilim: Kilim is a Java framework for writing lightweight, concurrent, and high-throughput applications. It uses bytecode instrumentation to transform ordinary Java classes into cooperative multitasking actors. Kilim provides an efficient implementation of the Actor model with minimal overhead.

## Bad
- Overhead: The Actor model introduces some overhead compared to lower-level concurrency models. Actors communicate by message passing, which involves the creation, sending, and processing of messages. This overhead can impact performance, especially in systems with high message rates or when actors need to communicate frequently.
- Complexity: While the Actor model provides a higher-level abstraction for concurrency, it also introduces additional complexity. Designing and implementing actors and their message-based communication requires careful consideration. Managing the lifecycle, supervision, and coordination of actors can be challenging, particularly in large-scale systems. Actors must be designed with proper error handling and recovery mechanisms to ensure fault tolerance.
- Asynchronous Programming: The Actor model heavily relies on asynchronous programming. While this can improve system responsiveness and scalability, it also introduces challenges in terms of reasoning about and debugging asynchronous code. Proper handling of asynchronous operations, such as callbacks and futures, is necessary to ensure correct behavior and avoid issues like race conditions and deadlocks.
- Message Passing Overhead: The communication between actors through message passing may introduce latency and overhead. Actors communicate by sending and receiving messages, which involves serialization, network communication (in distributed systems), and message queueing. These additional steps can impact overall system performance and throughput, particularly in scenarios with strict latency requirements.
- Shared State Coordination: While the Actor model helps in managing concurrency and isolating actor state, it can still face challenges when it comes to coordination of shared state. Actors may need to coordinate their activities or share resources, which requires careful synchronization. Ensuring proper consistency and avoiding data races when actors access shared state can be complex and may require additional synchronization mechanisms.
- Learning Curve: Adopting the Actor model requires a shift in programming mindset compared to traditional sequential programming or other concurrency models. Understanding the principles of message passing, actor supervision, and error handling may involve a learning curve for developers who are new to the model. This can impact the development time and require additional training or expertise.
## When to use 
- Complex Workflows: 
  - Actors are advantageous when dealing with complex workflows or business processes. Actors can represent individual steps or components within a workflow, and their message-based communication facilitates coordination and orchestration. This makes it easier to model, implement, and modify complex interactions and business logic.
- Scalability:
  - The Actor model promotes scalability by allowing easy distribution of actors across multiple nodes or machines. The message passing nature of the model enables workload distribution and load balancing, allowing systems to scale horizontally as the demand increases. Actors can dynamically spawn additional actors to handle increased load, providing elasticity and scalability.
- Fault Tolerance:
  - Actors offer built-in fault tolerance mechanisms, making them suitable for systems that require high reliability. Actors can handle failures within their own scope, allowing for isolation and recovery. Supervision strategies can be defined to manage the lifecycle of actors, automatically restarting failed actors or taking appropriate actions in response to failures.
- Stateful Components: 
  - Actors are beneficial when you need to manage complex state within individual components. Actors encapsulate their state and provide a clear boundary for state management. This makes it easier to reason about the behavior of individual components and simplifies the handling of mutable state, minimizing the risk of data races and ensuring data consistency.
- Concurrent Processing:
  - When you need to design systems that can efficiently process multiple tasks concurrently, actors provide an excellent model. Each actor can independently process messages, allowing for parallel execution and efficient utilization of resources. Actors can handle both CPU-bound and I/O-bound tasks effectively.

## Alternatives to actor model 

- use lower level concurrency models, like Threads or executer services 

## Difference between 

- Concurrency Model: 
  - The Actor model focuses on concurrency and encapsulates both state and behavior within actors. Each actor is an independent entity that processes messages asynchronously. Actors can communicate with each other by exchanging messages. 
  - message queues primarily focus on message passing between different components or systems. Message queues provide a way to decouple the sending and receiving components, but they do not define any behavior or state within the components themselves
- State Management: 
  - In the Actor model, each actor has its own internal state that can be updated and maintained. Actors can encapsulate their state and behavior, allowing for more fine-grained control and flexibility in managing concurrent operations. 
  - message queues typically do not manage state directly. They serve as a communication channel, enabling components to pass messages back and forth without explicitly managing state within the message queue itself.
- Concurrency Control:
  - Actors in the Actor model inherently handle concurrency through message passing and asynchronous execution. Actors can process messages concurrently, and their state is protected and accessed only through message exchange, providing built-in concurrency control.
  - In message queues, concurrency control needs to be implemented separately by the components that interact with the message queue. The message queue itself typically provides basic synchronization mechanisms, such as message ordering and delivery guarantees, but it is up to the components to handle concurrency appropriately. 
- Abstraction Level: 
  - The Actor model provides a higher-level abstraction that combines both behavior and state within actors. It allows for a more modular and encapsulated design, where each actor can have its own logic and state management. 
  - Message queues, on the other hand, provide a lower-level abstraction focused on message passing between components. They are often used as a communication mechanism between different parts of a system, but they don't provide the same level of encapsulation and behavior as actors do.
## Difference with event driven model 
- The Actor model emphasizes encapsulated actors with their own state and behavior, communicating through message passing. The Event-driven model focuses on events and event handlers, where events trigger asynchronous processing by relevant handlers.
- Unit of Concurrency: 
  - In the Actor model, concurrency is achieved through independent entities called actors. Each actor has its own state, behavior, and message queue. Actors communicate by asynchronously sending messages to each other.
  - the Event-driven model focuses on events as the unit of concurrency. Events represent occurrences in the system, and event handlers or callbacks are invoked to process these events.
- State Management: 
  - In the Actor model, each actor encapsulates its own state, which is not directly accessible by other actors. Actors can modify their state only by processing messages. This encapsulation provides a clear boundary for state management and helps in avoiding shared mutable state. 
  - In the Event-driven model, state management can vary depending on the specific implementation. Events may modify shared state directly, or event handlers may maintain their own internal state.
- Message Passing vs Event Handling: 
  - The Actor model relies on message passing for communication between actors. Actors send messages to each other's mailboxes, and the receiving actor processes the messages sequentially. 
  - In the Event-driven model, events are typically broadcasted or published to interested event handlers or subscribers. Event handlers are triggered asynchronously when relevant events occur, and they can handle events concurrently.
- Concurrency Control: 
  - In the Actor model, concurrency control is inherent in the message passing mechanism. Actors process messages sequentially, and only one message is processed at a time by an actor. This simplifies concurrency control and avoids the need for explicit synchronization in most cases.
  - In the Event-driven model, concurrency control needs to be explicitly managed, as event handlers may be triggered concurrently. Synchronization mechanisms like locks or other concurrency control mechanisms are often used to handle shared resources accessed by multiple event handlers.
- Granularity: 
  - The Actor model provides a higher level of abstraction, where each actor represents an autonomous entity with its own behavior and state. Actors encapsulate complex logic and state management. 
  - the Event-driven model provides a more low-level and fine-grained approach, focusing on individual events and their associated handlers. It allows for more flexible event routing and composition.
## Links 

- https://youtu.be/DCWo9DuywYo The Next Big Thing In Software Architecture • Dave Farley • GOTO 2023
