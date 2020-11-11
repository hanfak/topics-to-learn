# Alternatives to choosing microservices first when scaling

These are common sense techniques and rules of thumb that help pluck the low-hanging fruits of typical scaling problems, before going to microservices/cloud

Don’t try to “scale” like Google, or anyone else for that matter. It is always very specific to an organisation.



- Comparisons dont mean much
  - Example
    - An application that serves 1000 requests per second of static data is not the same as one that serves data from a database. Querying a database with a billion time series data points is not equal to doing a full text search on a billion rows, or even a fraction of that.
  - Comparisions only make sense within their specific environments.
  - Examples of how to scale, are generally not useful for your circumstances
  - Thus using someones example and saying it will work your system will not be useful

- Scaling starts with well built software.
  - Scaling starts bottom-up with good code and good software.
  - One moves on to scaling resources horizontally or vertically after exhausting all easy optimisations in application code.

- premature optimisation is bad
  - In the beginning, focus on writing good-enough software. Then refactor and improve as time progresses.
  - Trying to build for “web scale” on day one can turn out to be painful as the careful premature optimisations get thrown out of the window as the business and user requirements change unpredictably
  - not every piece of all software has to be low latency and high throughput to begin with.
  - On the other end of the spectrum is being lazy ignoring common sense principles leaving them for later.

- KISS, don’t be afraid, and boring > cool.
  - Dont worry or fear missing out on “cool” and advanced technologies
  - “Keep it Stupid Simple” is a paradoxical adage. It is conceptually so simple that it creates the irrational fear that complexity implies sophistication and simplicity implies primitiveness.
  - Complex technologies solve specific organisational problems more than generic technical problems.
  - using Kubernetes, can be used to primarily make application deployments uniform just as the process had started to grow complex, and not really to attain any sort of performance or scaling benefits
  -  frameworks and abstractions come with their own cost to pay, and probably would not be a sensible trade-off in a small organisation
  - Boring is generally battle-tested and well-understood sans novelty
  - what matters is quality software that can be run with as little headache as possible, not the frameworks or methodologies they’re deployed on.

- The bottleneck is almost always the database.
  - 98% (fictional) of all scaling bottlenecks stem from databases, and not the algorithms or data structures (which devs will prematurely optimise first)
  - In the face of a database bottleneck, every other optimisation in an application pretty much immediately becomes immaterial.
  - Example, A complex web framework in a complex language that can handle 500,000 “hello world” requests per second, when connected to a database that can only handle 1000 queries per second, can then only handle 1000 requests per second
  - If this database bottleneck cannot be improved, might as well use a simpler framework with less throughput to make life easy.
  - It is important to understand the global bottlenecks, which almost always are databases, before making fine-grained optimisations and decisions.

- RDBMS works, almost always.
  - 98% (fictional) of all business problems can be reduced to CRUD, represented as relational data that need ACID guarantees and reporting that can be easily expressed as SQL
  - Very few problems need map-reduce or schemaless storage, due to the fundamental nature of businesses and business data than any technical underpinnings.
  - When a Postgres node—with at least one replica for high-availability—with proper logical partitions and indexes can hold hundreds of billions of records, terabytes of data, and still perform well, there is not necessarily a need to look for a distributed database sacrificing crucial RDBMS business features at the peril of re-inventing them in application code.
    - When that hits a bottleneck, some re-structuring of data and a cluster may solve it for good
  - it is generally simpler to model and operate business data on battle-tested RDBMS and to rely on the strength of SQL than to reinvent shoddy RDBMS features in the application wasting valuable time.

- Remember to index
  - slow db can almost always be attributed to poor indexing, poorly constructed queries, or poorly designed schemas
  - Always exhaust all possible optimisations
    - the schema and data representation
    - indexing
    - query planning
    - database configuration—before going shopping for a whole new database system
  - Learn sql
    - you can move significant amounts of redundant business logic from the application code to the RDBMS, which is what it is designed to do in the first place
    - ORMs may be nice abstractions for simple use cases, but can rapidly turn into painful bottlenecks.
      - Either they generate sub-optimal queries, or force one to contort gymnastically to produce complex, optimised queries. Rather learn SQL than some esoteric ORM language.
  - Be careful in how you use sql
    -  not using composite indexes, or not writing queries with fields in the proper order to align with composites
    - using text values instead of enums
    - Abusing LIKE queries


- Don’t use an RDBMS
  - they are almost always the cause of bottlenecks in a typical database backed application than the application code itself.
    - The fewer the queries that an application makes to a database, the faster it gets.
  - Using CMS, like wordpress, makes it hard to handle traffic spikes as it issues dozens of queries to the database on every single page load.
    - Most business applications are unlike that. They are purpose-built and can afford to remodel queries and plan data better to reduce the number of roundtrips to the database on hotpaths,
  - If it is possible to combine multiple queries into a single query (nest, join, or using CTEs), it almost always gives a significant performance boost.
  - for insertions, updations, and deletions, if it’s not easy to combine queries, they can probably be batched and committed in one shot, avoiding multiple network round trips.

- Networking/IO is really hard. Network as little as possible.
  - In a complex software system, internal networking is also a manifestation of dependencies and the organisational structure.
    - There must be a mathematical model somewhere that describes the ridiculous ways in which systems fail with every addition of a networked dependency.
  - Networking makes software problems worse by piling on complexities of
    - bandwidth and congestion
    - routing
    - load balancing
    - service discovery
    - packet drops
    - timeouts and retries
    - port and descriptor exhaustions
    - kernel configuration
    - operational overheads
    - data serialisation and API woes
    - etc
  - There are of course platforms that promise to magically abstract all of this away, but there is always a cost to pay.
    - Who watches the watchmen?
  - Given that these complexities are applicable when just two networked services talk to each other
    - But there are always more components interacting
  - The common sense approach would be to have as few services and networked dependencies as possible.
    - Have as few networked interactions, especially synchronous API calls, and roundtrips on application hotpaths as possible.
  - It is far more productive to focus on scaling application and data than to waste time on avoidable networking complexities

- Connections are hard. Connect little, pool much.
  - A network connection’s capacity is only as good as
    - the upstream’s latency (time required for a single request)
    - throughput (number of requests processed in a given window)
    - concurrency (number of requests that can be processed simultaneously)
  - Example
    - a database with 10 concurrent workers that can each process one query per second. It does not matter if an application opens 100 or a 1000 connections to the database. Only 10 connections will actually be used, and only 10 queries will be processed in a second.
    - The rest of the connections are just unnecessary resource hogs.
    - a common mistake, setting large connection limits for networked systems like databases in hopes of better throughput. Always pool.
  - Opening and closing TCP connections have significant overheads. Making 10,000 HTTP requests to a service using 10,000 connections is slow, resource intensive, and unsustainable.
    - Depending on the speed of the service, this throughput can be achieved with a pool keep-alive of 100 connections, or even 10
    - For networked systems, be it RDBMS or web services, optimal connection pool sizes should be figured out by evaluating latency and throughput.
  - As request volumes grow, connection pools start becoming visibly latency sensitive.
  - Can have web services that handle hundreds of thousands of requests per second using a few hundred connections in a pool as long as the request latencies are constant
    - the slightest increase in the latencies immediately render these pools useless, as the number of requests that can be served on a single connection reduces drastically causing connection pools to grow.
    - the latency increase upstream indicates its inability to process more requests in the first place, which means, the growing pool only makes matters worse, overloading upstream
    - This is a deadlock with no out but for the upstream service to go back to processing requests at low latencies
      - fixed by restarting everything imaginable
  - Horizontally scaling may or may not help depending on where the bottleneck is, and how bursty the traffic spikes are.
  - magine this happening in a microservice mesh of dozens of services
    - Hard to sort out
    - Sophistcated observation and tracing systems help, but they also require maintenance and scaling

- Latency is THE metric.
  - “One request per second per connection” is a nice rule of thumb for visualising capacity and designing services and networks as illustrated in the previous sections.
    - The key here is the consistency of latency. As long as it’s guaranteed that a request will always take one second and not two, it is possible to have build capacity for scale.
    - If it is unpredictable, sometimes two seconds, and sometimes five seconds, the service is scale-dead on arrival.
  - hard problem where much of the engineering effort should be focused.
  - make sense to engineer top down.
    - If one wants to handle 1000 requests a second, that is, 1ms latency on one request, engineer things behind that request to get it to 1ms. Or, scale horizontally by having 10 copies of the service each which has a 10ms latency, at increased complexity and expenses.
    - trade off

- The Internet is the Wild Wild West.
  - Despite your system being well built, highly optimised, low latency service with high throughput that handles hundred thousand requests a second.
    - One million concurrent users start sending requests to it from wildly varying 3G, 4G, and broadband networks over HTTP connections.
    - The service will instantly respond to an incoming request on a connection, but the connection to the user over the internet is unpredictable
    - It may take 50ms or several seconds to write a response.
    - For this period, the connection is held hostage by the user’s poor network and it is happening with a million connections concurrently
  - A typical solution here is to deploy load balancer proxies (HAProxy, Nginx)
    - they do the dirty work of juggling a huge number of end user connections, maintaining a finite pool of keep-alive connections in the backend to the upstream service.

- Caching is a silver bullet, almost
  - RDBMS queries are expensive, multiple networked service lookups are expensive, computations are expensive, everything is expensive, until they are cached.
  - Even a poorly written application with a fast cache gets a chance to act like a well written application.
  - needs to be done aggressively.
  - Getting the data into a cache in the first place is the responsibility of an independent asynchronous service elsewhere
    -  Disk persistence is turned off on these cache instances to get better performance boost
  - how often does the data a user looks at on an application, change?
  - Even caching for a few seconds can make a big difference.
  - Nothing beats caching in RAM, but not everything can be cached in RAM.
    - What can be, the heaviest queries, or the most frequent responses, probably should be.
  - If possible, cache forever, as long as invalidating the cache does not become overly complex
  - Generally, it’s possible to cache all GET requests until a corresponding POST or PUT request on that resource internally invalidates the cache.

- Dumb caching is best caching.
  - dumb Caching
    - When a request looks up data in a cache and dumps it directly in the response
  - The caching logic has no understanding of the semantics or structure of the data stored and just does bytes-out
  - Dumb caches are nice as the application logic need not concern with parsing or constructing data, which in turn may become its own bottleneck.
  - may not be feasible everywhere

- Some application state may not be bad.
  - That services should be to be stateless is a sensible gospel.
  - That does not mean that an application can’t have significant ephemeral in-memory cache.
  - Example
    - Imagine a database table with 100K rows of data that rarely changes. A service queries one value from this table to fulfill incoming requests. What if the service, on boot, read the entire 100K rows from the database and put them in an in-memory map. Now the requests can do an in-memory map lookup, several orders of magnitude faster, with no dependency on the database. This is an ephemeral state that can be thrown away. On the rare occasion when the database changes, simply restarting the application can replenish the cache.

- HTTP APIs can be E-Tagged (304)
  - Client-side HTTP caching (JS, PNG, CSS …) is what underpins the large scale scaling of content delivery and bandwidth savings on the WWW.
  - The browser caches a file, stores a hash, the E-Tag, and checks with the server if the file has changed by sending the E-Tag.
    - If it hasn’t, the server responds with 304 header with no actual data instructing the browser to use the cached version.
  - This works beautifully for HTTP APIs too
  - How
    - We send an E-Tag with all the HTTP API responses from server.
    - The browser automatically does the rest.
    - On the server side, there is a cache map that maintains the E-Tags per user per resource.
    - This tag is deleted when the cache becomes invalid, forcing a full HTTP 200 response the next time there’s a request.

- Serialisation is expensive
  - converting a native data structure into JSON, or any other format, is an expensive CPU-bound operation.
    - The bigger the payload, the slower it gets.
  - in a garbage collected (GC) language, it can generate significant amounts of garbage creating GC pressure that can cause global slowdowns in the application.

- Allocation is expensive
  - Memory allocation is expensive, especially in GC languages.
  - if services are mostly being IO-bound and not heavy on memory, they are unlikely to run into any GC induced performance issues
  - Learn to write good high productive code in the language you use
  - On hot paths, allocate as little as possible, re-use byte buffers, try and avoid unnecessary byte-string conversions, throw-away pointers, memory escaping from the stack to heap

- Multi-threading and concurrency are necessary, but hard
  -  If a service can provide X throughput with one thread, and 2X with two threads, it is a no-brainer to do it,
    - as long as the complexity of the multithreading logic does not outweigh the performance benefit.
    - Otherwise, it may be easier to run the two copies of the service.
  - Concurrency can be used in interesting places other than just networking
    - ie reading lines of json from files into database after serilising
      - solution,  a program that reads the file serially with one reader goroutine/thread and feeds lines to N concurrent goroutines (one per available CPU on the system), each of which does computationally heavy operations, and writes the results concurrently into a writer goroutine that feeds it into the database.

- Some technologies are genuinely slow. Use fast technologies.
  - Some languages and frameworks are slow
    - ok as long as they are used to build applications that do not need to serve low latency, high throughput requests without expensive and complex setups
  - but if you expect it to increase  in performance or scale later on
    - you are not using the right tool for the job
    - fighting against it, engineering complex solutions rather than building features
    - Should rewrite in tech which is more suited for your needs
    - or choose a suitable tech, before starting knowing the potential needs of the systems
  - Often, picking the right tool for the job, even if it means learning something new, can pay off in a big way
  - If need to use a slow technology, then use it aysnchronously (ie queues)
  - it is generally better to avoid large frameworks in applications
    - when it is time to dive into the application looking for micro-optimisations, the framework will get in the way.
    - sing replaceable libraries and composing them avoids framework-lockins that impede optimisations.

- Scaling horizontally, vertically, and “enterprisely”.
  - scaling vertically
    - adding a few CPUs or extra RAM
    - if this scales a service for a long time, that would be the path of least pain.
    - this is meant for sensibly built software
  - “Industry-leading”, “enterprise-grade” applications that need 128 CPUs and 512 GB RAM to service 2000 requests a second, scale “enterprisely”
    - This can cost more to scale vertically, as hardware will be more expenise to see benefits or custom built
  - Scaling horizontally, excluding high-availability scenarios, is far more complex as all the aforementioned networking pain comes into play
    - One would much rather optimise software and database dependencies, scale vertically as much as possible,

- Human impediment.
  - Sometimes (often), a managerial bottleneck is a bigger impediment to common sense scaling than network IO—a lead who pushes a distributed NoSQL database where an SQLite file is sufficient, or a service mesh of microservices instead of a couple processes behind Nginx, or a quantum computer instead of a $5 EC2 instance
  - Or it could be a developer who bought into the hype of a particular technology.
  - Non-technical decision makers with technical decision making powers, or overly biased technical people, unfortunately, are scalings problem for which there are no technical solutions.
  - Technical descisions should be based on and made by technical people
