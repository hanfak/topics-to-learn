# Projects and Software types

What an application is:
  - a model of the rules or “policies” that govern the business in order to make it easier for the users to interact with them.


## Greenfield

## Brownfield

## Enterprise software

- The display, manipulation, and storage of large amounts of complex data.
- The support and/or automation of business processes that rely on this data.
- used by Business
  - used by other areas of business
- makes or saves money for the business
- https://softwareengineering.stackexchange.com/questions/141411/what-is-enterprise-software-exactly
- enterprise software usually involves access to persistent data. There's often a lot of data, with multiple users trying to access it concurrently. Enterprise applications usually need to integrate with other systems.
- the tools, patterns, and languages used tend to make collaboration, security, stability and scaleability a priority
- Enterprise application software is typically hosted on physical servers. The software then relies on a computer network to connect to its many users. Some parts of the software may also rely on intranet and occasionally internet connections. Because enterprise software installs directly on organizational servers, the connection is generally more private and secure.
- databases in enterprise application software are meant only for the single enterprise, so other groups aren’t sharing a database and draining its processing capabilities.
-  is typically owned outright, giving users much more ability to customize it. Enterprises often have in-house developers and programmers tweak or overhaul the software to make it match enterprise needs. It’s also always malleable – if a new enterprise problem comes up, programmers can implement a new solution within the existing software.
- Enterprise software is meant for large businesses that require software that can scale with the needs of the business. Enterprise software, therefore, needs to be more powerful than the software sold to smaller businesses
- tailored towards ensuring maximizing performance at low costs.
- a piece of software provides enough confidence for companies to run the most critical parts of their business with it.
- https://www.aoe.com/en/enterprise.html
- http://tractsystems.com/what-is-enterprise-grade-software/
- https://www.bmc.com/blogs/enterprise-application-software-defined-how-is-it-different-from-other-software/
- https://www.cio.com/article/2439502/what-is-erp-key-features-of-top-enterprise-resource-planning-systems.html
- https://softwareengineering.stackexchange.com/questions/141411/what-is-enterprise-software-exactly
- https://codeburst.io/enterprise-software-is-the-hardest-software-to-write-c76d59725f3
-https://www.bmc.com/blogs/enterprise-application-software-defined-how-is-it-different-from-other-software/

### Common features

- Can be accessed by users for business purpose
- Integration with other apps
  - types
    - internal (Same department, other department)
    - external/3rd party
    - Human(user, support, devs, business), computer
  - via
    - HTTP (REST/Webservice/soap/graphql)
    - messaging services (jms/activemq)
    - Hessian
    - file exchange (ftp)
    - shared databases
    - email
- Designed to be modified to meet needs of business
- Reporting off data for business and functionality
  - Data most important and valuable resource that comes from the use of this application
  - Data warehousing
- Auditing data
- Improving efficiencies in the data, no repeated data
- Can be integrated with current business services
- Monitoring to diagnose issues and makes sure app is running and alerting if something is wrong or about to go wrong
  - via metrics, status pages and probes, logging
- Availability & Resilancy
  - does not fall over or break easily
  - Can be fixed easily  (the whole app or a specific action that failed)
  - run on many servers and/or in different locations
- Can handle multiple users
- Can handle user access for parts or whole of system
  - authorization - who can do what in app
  - authentication - who can access app
- Can handle lots of actions, calls to the system (transactions)
  - Use of concurrency and parallel techniques
  - scalable application (ie increased replicas)
- Can handle high intensive operations (calls to the systems) within agreed sla (service level agreements) timelimits
  - expensive calls to 3rd parties waiting for the response
  - calls to long processing services (internal or external)
  - Use of messaging protocols and patterns
    - aysnc integration
  - Use of concurrency and parallel techniques
- Secure
  - encrypted passwords/usernames for database, version control, logs etc
  - certificates
  - Access to servers and database with necessary permissions
  - GDPR
  - Monitors traffic, access logs
- Well tested
  - Automated
  - Manual
- Automated tasks using a scheduler
- Batch tasks to be done immediately or at specific times, done sync or async/concurrently
  - Use of a queue
- Can be user facing (gui) or apis/services, which interact with each other.
- Translation from one format to another, with validation and filtering, so that one part of the organisation can understand and use it.
- Buisness rules applied
  - happy paths
  - sad paths
- Does not break easily
  - handles exceptions gracefully
- Deployment
  - deployed to various environments for testing and prod releases (canary release)
  - make sure the release passes through stringent controls
  - app meets deployment requirements
  - does not break systems when rolled out, can be roll backed
  - properties/config for different environments
  - database
  - Can be deoloyed with little to no down time
- Well documented
- Code modular, maintainable and extendable
  - Easy for the business to add or change features, fix bugs within an acceptable time frame instead of rewriting it
- Decision on design, code, integration etc are made with
  - long term lifespan view,
  - policies of other departments in specifiying, making, testing, releasing and maintaining it, are followed,
  - Users of app needs are met
    - ie clients, business, laws and commissions

### Links

- https://tallyfy.com/enterprise-application/
- https://www.forbes.com/sites/adrianbridgwater/2019/03/02/what-makes-an-app-an-enterprise-application/


## Consumer/application software

- the day-to-day software we rely on to create documents, databases, spreadsheets, presentations, graphics, and more. We use application software, often shortened to applications or apps, to complete a function or even play a game. Enterprise application software falls into this category, as its function is to support the mission of a large enterprise.
- normal software would be the software made with individuals in mind, i.e. retail software or web applications targeting the general populace. Its success depends on how well it is received by users who in most part are offered a ready-made, 'standard issue' product. The development is an investment and the revenue comes from individual product or ad space sales.

### Individual user

- Web apps, Microsoft office
- Not crtical for running a business
-

### Business/organisation user

- Enterprise applications
- used by different parts or people of the business, ie support, reporting, processing

## System software

- the software programs that help the computer run, like the operating system. Without systems software, we would have to manually enter directions for each task we want a computer to complete. Examples of systems software include Microsoft Windows, Apple’s OS, and others.

## Middleware

- https://stackoverflow.com/questions/2904854/what-is-middleware-exactly

## Front end

## Back end

## web services

- A web service is a service that can be called by an application. These web services are separate programs that are independent from other applications and can be run on different machines.
- A web service exposes an API (Application Programming Interface) to communicate over a network usually through HTTP (Hyper Text Transfer Protocol). HTTP is an application protocol often used for communication between a web-client and a web-server. A web service exposes a port that gives other programs access to its functionality.
- https://www.javacodegeeks.com/2019/04/web-services-interview-questions-answers.html

## web applications/ web sites

## soap

## SaaS

- https://en.wikipedia.org/wiki/Software_as_a_service

- SaaS is a popular option for users that need to take care of a very specific purpose. In this software model, users typically rent the software, never owning it. SaaS is often hosted in the cloud, requiring users be connected to the internet to use the software and access the data. (Because of this SaaS can also be known as cloud applications.) But, cloud hosting also means that users can access the software widely, from computers, tablets, and sometimes even smartphones. Popular examples of SaaS include Slack, Salesforce.com, Dropbox, and Zendesk
- its drawbacks may include lack of customization and database maneuvering. The inability to customize this software means it often cannot be specific enough to large-scale, enterprise-wide missions

## PaaS

- https://en.wikipedia.org/wiki/Platform_as_a_service

## FaaS

## Mobile apps

## desktop apps

## Links

- https://spin.atomicobject.com/2015/10/29/software-project-classification/
- https://www.zdnet.com/article/the-difference-between-consumer-enterprise-software/
