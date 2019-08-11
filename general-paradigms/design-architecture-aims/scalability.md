
As the system grows (in data volume, traffic volume, or complexity), there should be reasonable ways of dealing with that growth

Reliability can be impacted by increase in load the system is under. It is always best to design for load increase when it is necessary, and not over engineer solutions in anticipation as this may never happen and waste of time (ie Agile way).

Example of load:

- Concurrent users increases
- Processing of much larger volumes of data

Scalability is the term we use to describe a system’s ability to cope with increased load

Deal with the following questions:

- “If the system grows in a particular way, what are our options for coping with the growth?”
- “How can we add computing resources to handle the additional load?”

Load can be described with a few numbers which we call load parameters. These parametes are specific to your system.

What are the bottlenecks that affected by load?

Examples:

- Requests per second to a web server
- the ratio of reads to writes in a database
- the number of simultaneously active users in a chat room
- the hit rate on a cache

Where load matters:

- average use case of system
- Specific use cases

Need to investigate, get data/metrics on what the curent load is, what are the trends.

Example of investigations:

- When you increase a load parameter and keep the system resources (CPU, mem‐ ory, network bandwidth, etc.) unchanged, how is the performance of your system affected?
- When you increase a load parameter, how much do you need to increase the resources if you want to keep performance unchanged?

**Throughput** is a measure of how many units of information a system can process in a given amount of time. examples:

- the number of records we can process per second
- the total time it takes to run a job on a dataset of a certain size.

The **response time** is what the client sees: besides the actual time to process the request (the service time), it includes network delays and queueing delays.

- use of median and percentile to measure it, rather than average.
  - the mean is not a very good metric if you want to know your “typical” response time, because it doesn’t tell you how many users actually experienced that delay.

**Latency** is the duration that a request is waiting to be handled—during which it is latent, awaiting service.

- Is Latency or response time affected by increased loads?

Percentiles are often used in **service level objectives (SLOs)** and **service level agreements (SLAs)**, contracts that define the expected performance and availa‐ bility of a service.
  - Example: An SLA may state that the service is considered to be up if it has a median response time of less than 200 ms and a 99th percentile under 1 s (if the response time is longer, it might as well be down), and the service may be required to be up at least 99.9% of the time.

Queueing delays often account for a large part of the response time at high percentiles. As a server can only process a small number of things in parallel (limited, for example, by its number of CPU cores), it only takes a small number of slow requests to hold up the processing of subsequent requests—an effect sometimes known as *head-of-line blocking*.

Even if those subsequent requests are fast to process on the server, the client will see a slow overall response time due to the time waiting for the prior request to complete. Due to this effect, *it is important to measure response times on the client side*.

Solutions:

- Need a different architecture.
- **Scaling up** (vertical scaling, moving to a more powerful machine) and **scaling out** (horizontal scaling, distributing the load across multiple smaller machines).
  - Distributing load across multiple machines is also known as a **shared-nothing architecture**.
  - A system that can run on a single machine is often simpler, but high-end machines can become very expensive, so very intensive workloads often can’t avoid scaling out.
  -  Make it elastic, meaning that they can automatically add computing resources when they detect a load increase, or make it scaled manually (a human analyzes the capacity and decides to add more machines to the system).
    - elastic for highly unpredictable loads
    - manual simpler and easier to manage
- Different solutions to handle 100,000 requests per second, each 1 kB in size, compard to a system that is designed for 3 requests per minute, each 2 GB in size—even though the two systems have the same data through‐ put.
