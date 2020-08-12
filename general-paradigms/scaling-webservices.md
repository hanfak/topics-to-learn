# Scaling Webservices

- Where most of your business logic will live.
- consider whether you need them in the first place and what tradeoffs you are willing to make.
- benefits such as
  -  promoting reuse
  - higher levels of abstraction
-  drawbacks such as
  - higher up-front development costs
  - increased complexity

## Designing Web Services

- Need for web services
  -  to expose alternative ways to interact with web applications by providing different types of application programming interfaces (APIs)
  -  the need for integration and reuse grew with size of applications
  - Different clients/UIs (web/mobile etc) sharing the same logic/apis

### Web Services as an Alternative Presentation Layer

- the api is the presentation layer
- To develop web services (monolothic way)
  - to build the web application first and then add web services as an alternative interface to it.
  - your web application is a single unit with extensions built on top of it to allow programmatic access to your data and functionality without the need to process HTML and JavaScript
    - web application is developed, deployed, and executed as a single unit
    - web services would be implemented as a set of additional controllers and views, allowing clients to interact with your system without having to go through html
  - ie first build the ui (html/css etc), and your business logic (mvc framework)
    - After the core functionality was complete, you would then add web services to your web application when a particular need arose
  - Benefits
    - you can add features and make changes to your code at very high speed, especially in early phases of development
      - Not having APIs reduces the number of components, layers, and the overall complexity of the system, which makes it easier to work with
        - reduce integration costs
    - Easy to get MVP out there
    - defer implementation of any web service code until you have proven that your product works and that it is worth further development
    - not every web application needs an API, and designing every web application with a distinct web services layer may be just unnecessary overengineering
    - Good for simplest systems
  - Drawbacks
    - For complex systems not the best
    - Not great for scalability
    - Not great for long term maintenance
    - all of the code in a single application, you now have to develop and host it all together
      - ok for small team working on it, but once the team expands it becomes difficult to work on, merges take longer
      - as everyone needs to understand the whole system and make changes to the same codebase.
    - There will be potential future costs as the product becomes more successful
  - As the applicaiton grows in size
    - flexibility of making quick, ad hoc changes becomes less important
    - the separation of concerns and building higher levels of abstraction become much more important

### API First

- implies designing and building your API contract first and then building clients consuming that API and the actual implementation of the web service
  - Does not matter what is built first, the client or server
-  a solution to the problem of multiple user interfaces
  - Allows mutliple clinets to access the service via a programmatic interface
- All clients will use a single api to provide the business logic
-  API-first is better suited for more mature systems and more stable companies than it is for early phase startups.
- Benefits
  - REduces duplication of logic handled for different clients
    - you only need to maintain one copy of that code, easy to change and add features
  - Encapsulates logic, so clients can focus on their needs
    - changing client code becomes easier
  - Easier to scale
    - use functional partitioning and divide your web services layer into a set of smaller independent web service
    - Different teams can work on different clients and services
    - Decouples layers, easier to understand system and changes will not have  affects on other layers
    - can scale services and clients differently to meet their needs
    - different services and clients can use different technologies to better meet their needs
- Drawbacks
  - Difficult to implement
  - over engineering is an issue
  - integration, monitoring and deployments can be an issue (cost, time etc)
  -  requires more planning, knowledge about your final requirements, and engineering resources
  -  requires more planning, knowledge about your final requirements, and engineering resources

### Pragmatic - combination

- think of a web services layer and service-oriented architecture from day one, but implementing it only when you see that it is truly necessary
  - when you see a use case that can be easily isolated into aseparate web service and that will most likely require multiple clients performing the same type of functionality, then you should consider building a web service for it.
  - when you are just testing the waters with very loosely defined requirements, you may be better off by starting small and learning quickly
- Which approach depends
  - Money/funding
  - Stage of development
- if you go for that hybrid approach, you are in for a game of tradeoffs and self-doubt—either you risk overengineering or you make a mess
  - you are likely going to end up with a combination of tightly coupled small web applications of little business value and a set of web services fulfilling more significant and well-defined need

## Types of Web services

### Function-Centric Services

-  is to be able to call functions’ or objects’ methods on remote machines without the need to know how these functions or objects are implemented, in what languages are they written, or what architecture are they running on.
- each function  can take arbitrary arguments and produce arbitrary values
- difficult to implement across programming languages, central processing unit (CPU) architectures, and run-time environments, as everyone had to agree on a strict and precise way of passing arguments, converting values, and handling errors
  - Need to handle resource locking, security, network latencies, concurrency, and contracts upgrades.
  - all focusing on client code being able to invoke a function implemented on a remote machine
- Tech examples
  - Common Object Request Broker Architecture (CORBA)
  - Extensible Markup Language – Remote Procedure Call (XML-RPC)
  - Distributed Component Object Model (DCOM)
  - Simple Object Access Protocol (SOAP) (became standard)
    - Good extensibility and backing
    - use of xml to describe and encode messages
    - use of http to transport request and response
    - SOAP’s advanced security and distributed computing features
    -  it allowed web services to be discovered and the integration code to be generated based on contract descriptors themselves
    - Implementation example
      - web service provider exposes a set of XML resources, such as Web Service Definition Language (WSDL) files describing methods and endpoints available and definition of data structures being exchanged using XML Schema Definition (XSD) files.
      - These resources become the contract of the web service, and they contain all the information necessary to be able to generate the client code and use the web service.
      - You would use a client library which downloads the contract, convert xml to java classes, handle the network calls deserializations
    - extensibility
      - a lot of ws-specifications were created
      - which lead to integration between different development stacks became more difficult, as different providers had different levels of support for different versions of ws-* specifications.
    -
    - Dynamic language users found it harder to use SOAP web services
      - lack of tooling or support/funding/time to create tooling
      - Led to web tech being excluded from soap
      - Thus creating JSON and use of REST
    - Issues with SOAP
      - cannot use HTTP-level caching (not cached in a reverse proxy)
        - SOAP requests are issued by sending XML documents, where request parameters and method names are contained in the XML
        - Since the uniform resource locator (URL) does not contain all of the information needed to perform the remote procedure call, the response cannot be cached on the HTTP layer based on the URL alone
      - some of the additional ws-* specifications introduce state into the web service protocol, making it stateful.
        - As soon as you begin supporting things like transactions or secure conversation, you forfeit the ability to treat your web service machines as stateless clones
      - Not the best for a start up
      - Complexity
        - Different SOAP services have different conventions
      - SOAP is on the decline, more people moving to REST
        - this also leads to lack of support and fixes

### Resource-Centric Services

- each resource can be treated as a type of object, and there are only a few operations that can be performed on these objects
  -  CRUD
  - You model your resources in any way you wish, but you interact with them in more standardized ways.
- REST is an example of this type and now defacto standard of web services
- REST services use URLs to uniquely identify resources.
  -  Once you know the URL of a resource, you need to decide which of the HTTP methods you want to use.
    - In general, the GET method is used to fetch information about a resource or its children
    - the PUT method is used to replace an entire resource or a list by providing a replacement
    - POST is used to update a resource or add an entry
    - DELETE is used to remove objects
- JSON is defacto standard of REST
- Benefits of REST
  - the structure of REST web services is usually predictable, which also makes it easy to work with, due to limited number of HTTP methods
  - Lightweight
    - It’s basically just an HTTP server with a routing mechanism to map URL patterns to your code
    - Most frameworks make it easy to create
    - dont have to manage complex contracts like WDSL or xsd
  - less sophisticated than SOAP
    - To allow authorized access to REST resources, web services usually require authentication to be performed before using the API.
      - The client would authenticate (ie via OAuth), then provide the authentication token in HTTP headers of each consecutive request
      - Use of TLS in transport ie HTTPs
    - Stateless and GET request can be cached
      - Easier to scale
      -  traffic for the most popular resources to be offloaded, ease the load on services
  - Used by most web technologies
onto reverse proxies
- Drawbacks of REST
  - Less strict
    - allowing nonbreaking changes to be released to the server side without the need to recompile and redeploy the clients
  - Clients will not be able to auto-generate the client code or discover the web service behavior
    - Can have contract testing to warn about this
  - less sophisticated than SOAP
    - can make it harder to integrate with more complex secruity measures ie exactly-once delivery semantics
  - Less mature or feature rich
- if all you need is to expose a web service to your mobile
clients and some third-party websites, REST is probably a better way

## Scaling REST services

- tactics in general
  - slice your web services layer into smaller functional pieces
  - to scale by adding clones
- The key to scalability and efficient resource utilization is to allow each machine to work as independently as possible
  -  For a machine to be able to make progress (perform computation or serve requests), it should depend on as few other machines as possible

### Keeping Service Machines Stateless

- make all of your web service machines stateless.
- need to push all of the shared state out of your web service machines onto shared data stores like
  - object caches
  - databases
  - message queues
- Benefits of statelessness
  - distribute traffic among your web service machines on a per-request basis.
    - can deploy a load balancer between your web services and their clients, and each request can be sent to any of the available web service machines
    - distributing requests in a round-robin fashion allows for better load distribution and more flexibility
  - As each web service request can be served by any of the web service machines, you can take service machines out of the load balancer pool as soon as they crash.
    - load balancers support heartbeat checks to make sure that web service machines serving the traffic are available.
    - LB can have automatic load sharing, so when heartbeat fails it will send traffic to other clones
      - will remove that host from the load-balancing pool, reducing the capacity of the cluster
      - but preventing clients from timing out or failing to get responses.
    - Allows technical support to look at what is wrong and fix it, or restart a clone
      - modern application/container management (kubentes) will create new clone if there are less then the desired amount required in config
  - can restart and decommission servers at any point in time without worrying about affecting your clients.
  - Allows for maintenance to be done easily without loss of service
    - LB allows for graceful shutdown, ie reducing load on a host until zero
  - able to perform zero-downtime updates of your web services.
    - an roll out your changes to one server at a time by taking it out of rotation, upgrading, and then putting it back into rotation.
    - If your software does not allow you to run two different versions at the same time, you can deploy to an alternative stack and switch all of the traffic at once on the load balancer level
  - able to scale your web services layer by simply adding more clones
    -  by adding more machines to the load balancer pool to be able to support more concurrent connections, perform more network I/O, and compute more responses (CPU time).
    - only assumption here is that your data persistence layer needs to be able to scale horizontally
  - Auto scaling can happen
    - Any time a machine crashes, the load balancer will replace it with a new instance
    - any time your servers become too busy, it will spin up additional instances to help with the load
- The only type of state that is safe to keep on your web service machines are **cached objects**, which do not need to be synchronized or invalidated in any way
  - As cache is disposable and can be rebuilt at any point in time, so server failure does not cause any data loss.
-  Any solution that requires consistency to be propagated across your web service machines will increase your latencies or lead to availability issues
  - To avoid, it is safest to allow your web service machines to store only cached objects that expire based on their **absolute Time to Live** property
  - Such objects can be stored in isolation until they expire without the need for your web services to talk to each other.
- Sharing state amongst webservice clones
  - Always question whether transactions or even locking is necessary
    - alternative
      - making your application handle failures gracefully rather than preventing them at all cost
      -  try to lean back on your data store as much as possible using its transactional support (support for Atomic operations)
  - Secruity
    - Clients will likely need some authenticaiton passed alongside it's request (ie token/cookie)
    - That token will have to be validated on the web service side, and client permissions will have to be evaluated in some way to make sure that the user has access to the operation they are attempting to perform.
    - You could cache authentication and authorization details directly on your web service machines, but that could cause problems when changing permissions or blocking accounts, as these objects would need to expire before new permissions could take effect
    - use a shared in-memory object cache and have each web service machine reach out for the data needed at request time. If not present, data could be fetched from the original data store and placed in the object cache.
      - will be able to easily invalidate it when users’ permissions change, as only a single copy
  - Resource Locking
    - can use distributed lock systems like Zookeeper
    - you should avoid resource locks for as long as possible and look for alternative ways to synchronize parallel processes.
    - Distributed locking is challenging, as each lock requires a remote call and creates an opportunity for your service to stall or fail.
      - increases your latency and reduces the number of parallel clients that your web service can serve
    - can sometimes use optimistic concurrency control where you check the state before the final update rather than acquiring locks, instead of resource locks.
    - consider message queues as a way to decouple components and remove the need for resource locking in the first place
    - it is important to acquire locks in a consistent order to prevent deadlocks
      - can prevent deadlocks, and increase availability
    -  to strike a balance between having to acquire a lot of fine-grained locks and having coarse locks that block access to large sets of data
      - acquire a lot of fine-grained locks, you increase latency, as you keep sending requests to the distributed locks service.
      - having many fine-grained locks, you also risk increasing the complexity and losing clarity as to how locks are being acquired and from where.
        - Can lead to deadlocks
      - using fewer coarse locks, you may reduce the latency and risk of deadlocks
        -  but you can hurt your concurrency at the same time, as multiple web service threads can be blocked waiting on the same resource lock
    - By using locks, all of your machines become interdependent, If one process becomes slow, anyone else waiting for their locks becomes slow.
    - You can use locks in your
      - scheduled batch jobs
      - crons
      - queue workers
    -  best to avoid locks in the request–response life cycle of your web services
  - application-level Transactions
    - Transactions can become difficult to implement, especially if you want to expose transactional guarantees in your web service contract and then coordinate higher-level distributed transactions on top of these services
    - **A distributed transaction is a set of internal service steps and external web service calls that either complete together or fail entirely. **
    - If Transaction fails, everything needs to be rolled back, so that all the actions never happenend in the first place
    - 2 Phase Commit (2PC) algorithm. Common
      -  notorious for scalability and availability issues
      - become increasingly difficult to perform as the number of services involved increases and more resources need to be available throughout the time of the transaction
      - the chance of failure increases with each new service
    - away from distributed transactions
    - Alternatives to distrbuted transactions
      - not support them at all
        - Rather have development speed, availability, and scalability
        - As long as core features are not impacted, and minor inconsistencies are ok, have eventual consistency
      - provide a mechanism of compensating transaction
        - **A compensating transaction can be used to revert the result of an operation that was issued as part of a larger logical transaction that has failed**
        - Each part of transaction is independent, is part 1 passes but part 2 fails, then only part 1 is reverted (some opposite action that returns part 1 to original state).
          - If part 1 fails, then original caller will fail, so part 2 would not be used
        - Benefits
          - web services do not need to wait for one another
          - they do not need to maintain any state or resources for the duration of the overarching transaction
          - Each of the services responds to a single call in isolation
          - Only the coordinating web service becomes responsible for ensuring data consistency among web services
          - can often be processed asynchronously by adding a message into a queue without blocking the client code

### Caching Service Responses

- Use of HTTP protocol caching
- The HTTP protocol requires all GET method calls to be read-only. Can cache the response in a proxy/clients and web service calls can be skipped
- Need to make sure GET requests are idempotent and nothing is affected (ie state/db change)
- sometimes business needs prevents caching, as the needs for logs (which are updated when request hits service) are used for business reports
- Can also be affected by object caches on the service, which are updated and another service uses this updated cached object which could be different
- Authentication via tokens in headers
  - Would need to build cache key on url and header token (composite key) to make sure users only see what they should
  - But can be wasteful, if two different users have same authentication for same resource
- make as many of your resources public as possible
- To be able to scale using cache, you would usually deploy reverse proxies between your clients and your web service.

### Functional Partitioning

- functional partitioning can be thought of as a way to split a large system into a set of smaller, loosely coupled parts so that they can run across more machines rather than having to run on a single, more powerful server.
  - For  web services
    - is a way to split a service into a set of smaller, fairly independent web services, where each web service focuses on a subset of functionality of the overall system
    - isolating subsets of functionality that are closely related, and extracting that subset into an independent subsystem
- Rather than having a single large and potentially closely coupled web service, you would end up with two smaller, more focused, and more independent web services
  - lead to decoupling their infrastructures, their databases, and potentially their engineering teams
- Benefit
  - having two independent subsystems, you could give them at least twice as much hardware
    - esp separate data storage, each subsystem will have it's own db
    - esp good for relational db, as they are difficult to scale
  - development and changes can be made in isolation, affecting only one of the services
    - there is some coupling between services, but not that much
    - allows your technology team to grow
    - no one needs to know the entire system in detail to make chagnes
    - teams can take over one or more services
  - Each service can be scaled independently
    - Access patterns, availability and hardware needs are separated
    - Can scale to meet their own needs
    - no wasted resources for parts of a system like in monoliths
    - Different tech can be used for different services
- Challenge
  - partitioning too early
  - partitioning too much
  - new services that needs data and features from mulitple services
    - partition by what changes (volatility)
