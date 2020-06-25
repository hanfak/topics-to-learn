# Performance

- Hygiene factor
  - Nobody realises a high performant system, until it is not performing well enough (leads to compliants or user something else)

## Perceived Performance

- how quickly a system appears to perform its task.
- people have implicit expectations about performance, they are seldom expressed in hard figures
  - people tend to overestimate their own patience
  - Need to find these numbers, SLAs
- People tend to value predictability in performance
  - When the performance of a system is fluctuating, they remember a bad experience, even if the fluctuation is relatively rare
  - Need to implement consistent perfromance
- If a certain task takes a long time, it helps to inform the user about how long it will take.
  - ie use of progress bars
  - acceptance and wait time increases of users
- when the system seems unresponsive with no apparent reason, people get irritated very quickly.
- Increasing the real performance of a system can increase the perceived performance.
  - But real performance may not be able to increase (high cost/physics)
  - Use of splash screens (ie word) and progress bars
    - provide visual feedback that it is processing request
    - still users processing power
    - Use of ads (ie youtube to load videos)

##  Performance during infrastructure design

- Without proper design,  systems will respond to increased load with some degree of decreasing performance
- Design will help meet performance load increases
-  performance must be considered not only when the system works as expected, but also when the system is in a special state, ie:
  - Parts have failed
  - The system is in maintenance
  - A backup is performed
  - Batch jobs are running
- Calculating performance in the design phase is extremely difficult and very unreliable
  - Only on very small parts of the system, with predictable load, the performance can be calculated by analyzing each and every step of the implemented process.
  - Doing this is costly
- Ways of calculating performance
  - Benchmarking
  - Using vendor experience
  - Prototyping
  - User Profiling


### Benchmarking

- Comparing specs is not great to compare performance, Benchmarking is better
- A benchmark uses a specific test program to assess the relative performance of an infrastructure component.
- used to assess the performance characteristics of computer hardware or software
- Benchmarks provide a method of comparing the performance of various subsystems across different system architectures
- Be aware that benchmark programs heymeasure the raw performance, not taking into account the typical usage of such components.
- benchmarks are only useful for comparing the raw speed of parts of an infrastructure

### Using vendor experience

- Best way, let the vendor tell you
  - but must be exeperienced and trusted
- They know their products and gather stats
- they can provide tools, figures, and best practices to help design the appropriate infrastructure for their products.
- Can be used as consultants, but this costs

### Prototyping

- Use a prototype at an early stage of implementation
- ie by hiring equipment from suppliers, by using datacenter capacity at a vendor’s premise or by using cloud computing resources.
- To find potential performance issues as early as possible in the design process
- Prototyping should focus on those parts of the system that pose the highest risk
- A proof of concept (POC) should be used to test the most challenging parts of your solution early in the project.
  - Most people deal with easy parts then challenging parts later on
  - but challenging parts could lead to a delay in the project or even a halt.
- POC shows to both the project team and the customer that the project's highest risk has been taken care of

### User profiling

- used to predict the load a new software system will pose on the infrastructure, and to be able to create performance test scripts that put representative load in the infrastructure before the software is actually built
- NEed to have a good indication of the expected usage of the system
  - defining a number of typical user groups of the new system (also known as personas)
    - persona groups must be interviewed to understand how they will use the new system. producing a list of main tasks
    - For each of these tasks, estimations can be made on how, and how often they will use the system’s functionality to perform the task.
  - by creating a list of tasks they will perform on the new system.
  - Thus can figure out the amount data used accross network, hard disk written and read
  - This is just an idea, live functioning system the load on the
system for a specific task can be very hard to predict and will have:
    - many personas
    - complex tasks
    - tasks are spread in time
    - show hotspots (like starting the application or logging in, which typically happens at the start of the day)
    - High load time (sales)
    - the system can have background processes running

## Performance of a running system: Managing bottlenecks

- The performance of a system is based on the performance of all its components, and the interoperability of various components
  - measuring the performance of a system only has value if the complete system is taken into account.
  - ie building an infrastructure with really fast networking components has little benefits when the used hard disks are slow
- A performance problem may be identified by slow or unresponsive systems
  - usually occurs because of high system loads, causing some component of the system to reach some limit.
  - This component is referred to as the bottleneck
  - To find this bottleneck, performance measurements are needed
- Finding the bottleneck allows us to improve performance
- When a bottleneck is removed, usually another bottleneck arises
  - no matter how much performance tuning is done, there will always be a bottleneck
- bottlenecks are ok as long as it does not negatively influence performance of the complete system under the highest expected load


## Performance of a running system: Performance testing

- Benchmarking is a way to measure individual components, while system
performance tests measure the system as a whole
- Three major types of performance tests
  - Load testing
    - This test shows how a system performs under the expected load.
    - It is a check to see if the system performs well under normal circumstances.
  - Stress testing
    - This test shows how a system reacts when it is under extreme load.
    - Goal is to see at what point the system "breaks" (the breakpoint) and where it breaks (the bottleneck)
  - Endurance testing
    - This test shows how a system behaves when it is used at the expected load for a long period of time
    - finding out when the system will have performance degredation
    - Typical issues:
      - memory leaks
      - expanding database tables
      - filling disks
- How
  - Performance testing software typically uses one or more servers to act as injectors
    - each emulating a number of users, each running a sequence of interactions
  - A separate server acts as a test conductor, coordinating the tasks, gathering metrics from each of the injectors, and collecting performance data for reporting purposes
  - The usual sequence is to ramp up the load, by some factor
  - The test result shows how the performance varies with the load, given as number of users versus response time.
- Performance testing should be done in a production-like environment
  - Done in development environment usually lead to results that are highly unreliable.
  - To reduce cost, sometimes it is advisable to use a temporary test environment
    - with similar hardware as prod


## Performance patterns

### Increasing performance on upper layers (ie software)

- it is good practice to first check for performance optimizations in the upper layers
- Database and application tuning typically provides much more opportunity for performance increase than installing more computing power
- Application performance can benefit from
  - prioritizing tasks,
  - working from memory as much as possible (as opposed to working with data on disk)
  - making good use of queues and schedulers
- Improving performance of software only works when you have access to source code. For commercial off-the-shelf software, this is usually not feasible.
- Tuning the databases used by the application, by for instance adding indexes, can be an opportunity to significantly improve performance
- understand how applications work on a multithreaded system, and take advantage of multiple cores or multiple instances of applications

### Caching

-  improves performance by retaining frequently used data in high speed memory, reducing access times to data
- Different sources that provide data are slower than others
  - over the network is slower than ram
- Used for replacing reading from hard disk or from the network
- Disk caching
  - To speed up the reading of data from disk, disk drives contain cache memory
  - This cache memory stores all data recently read from disk, and some of the disk blocks following the recently read disk blocks.
    - When the data is read again, or (more likely) the data of the following disk block is needed, it is fetched from high speed cache memory.
  -  implemented in the storage component itself
    - cache used on the physical disks
    - cache implemented in the disk controller)
  - implemented in the operating system
  - **The general rule of thumb that adding memory in servers improves performance is due to the fact that all non-used memory in operating systems is used for disk cache**
    - Over time, all memory gets filled wit previously stored disk requests and prefetched disk blocks, speeding up applications

### Web proxies

- Type of proxy
- instead of fetching all requested data from the internet each time, earlier accessed data can be cached in a proxy server and fetched from there
- benefits:
  - users get their data faster than when it would be retrieved from a distant web server
  - all other users are provided more bandwidth to the internet, as the data did not have to be downloaded again

### Operational data store

- read-only replica of a part of a database for a specific use
- Instead of accessing the main database for retrieving information, often used information is retrieved from a separate small ODS database, not degrading the performance of the main database
- Have replica of the data in main db in the ODS

### Front-end servers

- In web facing environments storing most accessed (parts of) pages on the web front-end server (like the static pictures used on the landing page) significantly lowers the amount of traffic to back-end systems.
  - CDN
- Reverse-proxies can be used to automatically cache most requested data as well.

### In-memory databases

- used in situations where performance is crucial (like in real-time SCADA systems). Of course, special arrangements must be made to ensure data is not lost when a power failure occurs.

### Scalability

- indicates the ease in with which a system can be modified, or components can be added, to handle increasing load
- A system whose performance improves after adding hardware, proportionally to the capacity added, is considered to scale well
  - vertical scaling
- two ways to increase the scalability of a system:
  - Vertical scaling (also known as scale up) means adding resources to a single component in a system,
    - typically adding CPUs or memory to a server.
    - here is always a limit to how far a system can be expanded. physics
  - Horizontal scaling (also known as scale out) means adding more components to the infrastructure,
    - such as adding a new web server in a pool of web servers, or adding disks in a storage system.
    - drawback
      - larger numbers of components also mean increased management complexity, as well as a more complex programming model and issues such as throughput and latency between nodes.
      - pays off in the long run, as it is possible to scale up much more since there is a much higher upper limit.
    - works best when the system is partitioned
    - Parts of the system can scale independently of other parts of the system.
    - When more load is placed on the system, somewhere in the system a bottleneck will occur. At that point additional infrastructure components are added to cope with the load.
      - When needed, the system can be expanded further, either in the same tier, or on another tier
    - Doubling the number of components does not necessarily double the performance
      - Because of overhead
        - the extra scheduling needed inmultiprocessor systems, or buffering and link state issues in network connections
      - doubling components usually only provides about 70% to 80% performance increase.
      - Adding more components leads to even more diminishing returns.

### Load balancing

- Used to spread the load over various machines, horizontally scaled replicas
- A load balancer automatically redirects tasks to members in the server farm.
- checks the current load on each server in the farm and sends incoming requests to the least busy server.
  - Or using some algorithm
    - number of connections a server has
    - the measured response time of a server
- it increases availability:
  - when a server in the server farm is unavailable, the load balancer notices this and ensures no requests are sent to the unavailable server until it is back online again
- the availability of the load balancer itself becomes very important in this setting and load balancers are typically setup in a failover configuration.
- Load balancers must be identical
- The application running on a load balanced system must be able to cope with the fact that each request can be handled by a different server.
  - The application (or at least the load balanced parts of the application) must be stateless for this to work
-

### High performance clusters

- by combining many computer systems create high performance compute
- Usually a large number of cheap off theshelf servers are used, connected by high speed network
- used for calculation-intensive systems like weather forecasts, geological, nuclear, or pharmaceutical research
- The challenge is to have all systems doing useful calculations all of the time, without wasting too many resources and too much time communicating to other systems in the cluster.
- Many run on some varient of linux


### Grid Computing

- is a high performance cluster that consists of systems that are spread geographically.
  - The limited bandwidth is the bottleneck when architecting grid systems.
- Example
  - SETI@HOME
    - These types of grids utilize the unused computer time of PCs (for instance when the computer is displaying its screensaver).
- Secruity is important
  - PCs running calculations must be sufficiently secured against illegal use by third parties.
  - it should not be possible to alter data that is sent through the grid and the grid infrastructure must ensure the PCs calculate their tasks as expected
    - One way of handling this is to have each calculation executed twice, by two different PCs in the grid, and check for mismatches

### Design for use

- In general, it must be known what the system will be used for.
  - Different applications need to be built differently
- In some cases, special products must be used for certain systems
  - Real-time operating systems, in-memory databases, or even specially designed file systems can be a solution for special performance sensitive systems.
- Most vendors of databases, web servers, operating systems, and storage or network solutions have standard implementation plans that ar proven in practice.
  - In general, try to follow the vendor's recommended implementation.
  - good idea to have the vendors check the design you created.
- When possible, try to spread the load of the system over the available time.
  - ie Making certain that a backup job is not scheduled when some critical report is compiled is also a good idea
- To increase performance, sometimes it is possible to move rarely used data from the main systems to other systems.
  - Large databases are slower than small ones.
  -  Moving old data to a large historical database can speed up a smaller sized database.

### Capacity management

- This must be implemented if to guarantee high performance of a system in the long term
- the performance of the system is monitored on a continuous base, to ensure performance stays within acceptable limits. Trend analyses can be used to predict performance degradation before users start to notice it
- regular communication with the business allows systems managers to anticipate on business changes
