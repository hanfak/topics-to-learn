# Enterprise

- Enterprise computing is a broad concept that refers to all the necessary building blocks needed for establishing an enterprise application ecosystem that can support business operations more efficiently
- the platform includes
  -  computer hardware, networks, all supporting middleware software systems, and enterprise applications.

## Enterprise Software

- enterprise refers to a business organization in general.
- Software which the user and customer are distinct
- Enterprise software refers to a special class of software that enables running businesses on computers
- two categories:
  - infrastructure enterprise software
    - provides a platform on which application enterprise software is run.
    - All application server software and database server software belong to this category
    - examples
      - J2EE application server software such as BEA’s WebLogic, IBM’s WebSphere, and Microsoft’s .NET platform that includes many server components for different purposes.
      - Database server software such as Oracle, DB2 (IBM), and SQL Server (Microsoft).
      - Messaging software like kafka, activemq etc
      - specific OS or container management systems
  - application enterprise software
    - characterized by the business functions it supports and automates
    - typically depends on backend databases to support enterprise data management and information retrieval
    - An application server implements the business logic that may involve retrieving data based on authorized permissions, applying certain business rules such as data validation when inserting new data and modifying existing data, and so on
    - A Web server receives users’ requests, processes the requests, and renders the responses back to the user.
    - These application are surrounded by a firewall, as mainly used internally (employees or other internal systems)
      - external users will need to be given security access and specific privileges to access certain services
    - examples
      - Intranet portal application
      - Internal inventory management application
      - Sales order entry application
      - Accounting system
      - Production scheduling system
      - Customer relationship management system
      - Customer billing system
      - IT service management system


## Language requirements

- Nullable Types
  - Instead of having a pointer or reference to something that might be null, and occasionally throwing a NullPointerException or equivalent, the compiler can actually completely prevent code from ever trying to use a null pointer.
  - Work around, using Option type
- Green/Light Threads
  - When you’re trying to squeeze the most performance possible out of a server, you don’t want to rely on using individual OS threads for every task you’re performing (unless your server is performing extremely CPU-heavy work, which is a workload that doesn’t benefit from this feature). Instead it’s much more efficient to only create as many threads as there exist CPU threads, and then swap between a number of different tasks on each of those threads. These are often called green thread
  - async/await functionality
  - goroutines which are super-powered light threads that can even bounce between CPU threads
  - Actors which look close to the same thing, but they push some of the logic into the developer’s lap, instead of just allowing you to write code as if it’s imperative. This can improve flexibility at the cost of clarity of how the code will actually execute.
  - Vert.x that support event-based dispatch, to achieve the same performance advantages, but they require you to use callback-style syntax
- Resource Acquisition Is Initialization (RAII)
  -  pattern where you allocate a resource, perform operations within a block, and when the block exits the resource is released.
  -  Being able to allocate a mutex and be guaranteed that the mutex will be released, perform a database transaction, or perform file or network operations with a guarantee the file will be closed
  -  try-with-resources” pattern
-  Generics
-  Functional Method Chaining
  -  streams
-  
