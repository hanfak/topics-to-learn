# Enterprise

- Enterprise computing is a broad concept that refers to all the necessary building blocks needed for establishing an enterprise application ecosystem that can support business operations more efficiently
- the platform includes
  -  computer hardware, networks, all supporting middleware software systems, and enterprise applications.
- business computing is highly networked and distributed. It is also database intensive and requires that the state of data stored across multiple databases, across multiple computers, across multiple locations, remain accurate and synchronized at all times 
  - complex, specialized applications upon which modern corporations depend to run their businesses and interact with their customers
  
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
  - Involves, but not all features and at varying levels
    - critical functionality
    - Large amounts of data
    - large quantity of concurrently accessed data
    - large number of screens
    - integration
    - conceptual dissonance
    - complex logic and business rules

## What to think about

- Areas
  - How to represent the business entities (DDD)
  - How to persist it's state
  - How to code the business logic
  - How to guarantee data coherence
  - How to handle application distribution

## Patterns

- see [patterns](../../patterns/enterprise/README.md)

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

## Fallacies of enterprise computing 

### New technology is always better than old technology
- newer is not always better
- youth centric industry, leads to wanting to use new tech (exciting, not boring) rather than evaluating to find the best tech for the situation
- The idea of not wanting to fall behind
- Leads to rewrites with not obvious gain, and increase bugs and loss of features, maintaining multiple apps
- In this trap, if no negative thought is expressed about the technology
- No technology is never without its negatives
- force those advocating new technology to enumerate the benefits in concrete terms---monetary and/or temporal benefits, ideally, backed by examples and objective analysis of pros and cons.
- Ask 
  - When would I not use this?
  - What circumstances would lead me away from it?
  - When is using this going to lead to more pain than it's worth?
- 
### Enterprise systems are not "distributed systems"
-  any enterprise system is subject to the same fallacies as any other distributed system.
- Reliability, latency, bandwidth, security etc
- They need to be mitigated

### Business logic can and should be centralized
-  term "business logic" is way too nebulous to nail down correctly, and because business logic tends to stretch out across client-, middle- and server- tiers, as well as across the presentation and data access/storage layers.
-  Where do we enforce this particular rule?
  - Database 
    - schema can enforce it
    - ie size of field (ie name) can set size instead of allowing size to be bigger to allow for flexibility if requirements chagne
    - But this violates the rule that business logic should be in one place
  - Across multiple areas
    - UI - ie javascript on form, database - schema, coding rules in code
    - but this enforces if one area breaks, but has it spread out (DRY issues )
  - Avoiding putting in presentation layer
    - but this can lead to multiple round trips to check a form has correct data
- Source of this fallecy
  - from the old-style client/server applications and systems, where all the rules were sort of jumbled together, typically in the code that ran on the client tier. 
  - Then, when business logic code needed to change, it required a complete redeploy of the client-side application that ended up costing a fortune in both time and energy, assuming the change could even be done at all–the worst part was when certain elements of code were replicated multiple times all over the system. 
  - Changing one meant having to hunt down every place else a particular rule was–or worse, wasn’t–being implemented.
- the driving force behind "centralize your business logic" was really a shrouded cry for "The Once and Only Once Rule" or the "Don’t Repeat Yourself" principle.
  - Good rules of thumb, but taken to the extreme can lead to a whole load of issues
- one place where the "centralize only if it's convenient" rule has to be set aside is around validating inputs from foreign locations---in other words, any data which is passed across the wire or comes in from outside the local codebase.
  -  data should always be verified as soon as it reaches your own shores
  - for security 

### Data, object or any other kind of model can be centralized
- Having one domain model, is nice to have but has similar issues to having one database model
- One database model, promosied massive savings, 
  -  but resulting model was so complex and unwieldy that within a short period of time (usually measured in months) it was abandoned and/or fractured into smaller pieces so as to be usable.
  - Idea of dry, reusability
- Everything that everyone uses is one place, so lots of stuff, stuff that is not needed etc
  - leads to long load times from database or high latency as more data transfered over the wire
  - Clients will quickly start caching off only the parts they care about, and the centralized data model is essentially decentralized again.
- problem here is that different parts of the enterprise care about different aspects of a given "entity".
- Splitting data into normalised forms, can help
  - but leads to multiple joins. slow queries
  - what data to split on
-  the code that accesses the centralized data model often needs to be modified in response to "local" concerns
  - ie HR may suddenly require that "names" (which are common to the Person core table) be able to support internationalization, but Marketing is right in the middle of an important campaign, and any system downtime or changes to their codebase are totally unacceptable. Suddenly we have a political tug-of-war between two departments over who "owns" the schedule for updates, and at this point, the problem is no longer a technical problem whatsoever 
  - Same issue occured for schema based xml
- a domain model in the traditional DDD sense simply cannot be shared across language boundaries, no matter how anemic.
  - some form of language translation for local compilation, and these will almost always lose any behavior along the way---only the data types of the fields will be brought along
- Need to have multiple bounded contexts (either modular/microservices) and each have their own domain
  - this can lead to some duplication, but the domain knowledge is separate (ie person for HR and Marketing are different)
  - To get information from one bounded context leads to translation layer between apis - decoupling 

### The system is monolithic
- may have been true in older systems on mainframes
-  the whole point of an enterprise system is to integrate with other systems in some way, even if just accessing the same database
- the different parts of the system will need to deploy, version, and in many cases be developed independently of one another.
- Lead to microservices 
  - but implicitly creating dependencies between the microservices with no mitigating strategy to deal with one or more of those microservices being down or out.
  - Instead of dealing with the problems explicitly in a monolith (ie compliation) 
  - The problem occurs implicitly (At runtime), and is hidden

### The system is finished

-  is a constantly shifting, constantly changing environment.
- Nothing is ever finished
- always maintanence 
- recognize that systems need to be able to evolve effectively over time
  - needs to be built in 
    -  be built with an eye towards constant-modification and incessant updates.
  - impetus fo agile

### Vendors can make problems go away

-  they've never been able to do so except in some very narrow vertical circumstances.
- Always need to hack or build a solution on top, to fix the problem 
- Current idea of lifting and shifting to the cloud, does not magically guarentee anything
  - this generally lead to more work to get it working
- Vendors aim is to sell 
- Need to think carefully on using vendors, libraries and frameworks
- Integration issues
- Dont believe the hype


### Enterprise architecture is the same everywhere

- no one exerience in a one enterprise will make it easy for you to get up and running in another
- Alwasy different, need to learn
  - more experience makes it easier to learn and get effective faster, but not immediate
- Not all requirements are the same between enterprises
- enterprise architecture is highly context-sensitive to the enterprises for which it is being developed,
  - otherwise, someone would have created an product which could be used by all
  - partial solutions exists for part of the enterprises needs

### Developers need only worry about development problems

- Enterprise systems come with much higher criticality concerns than the average consumer software product.
-  If the company's e-commerce system crashes, literally thousands of dollars are potentially being lost per minute
  -  And that's not counting the cost of potential customer service costs or even lawsuits if an order is lost because the system went down mid-transaction and put the data into a corrupted or unrecoverable state. 
  - Nor does that consider the intangible costs that come into play when the news covers the outage in the public
  - Compared to an phone app, only that user will be affected
- Enterprise systems, by definition, have much higher reliability and recoverability concerns
  - costs more
  - So must be a first going concern of all
  - All other areas outside of development must be catered for and designed for by developers 
    - how the system is administered, deployed, monitored, managed, security etc
- It is never acceptable to find out about an enterprise system outage from your users.