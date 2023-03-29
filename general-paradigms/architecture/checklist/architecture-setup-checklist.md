# Checklist for new project

- [Checklist for new project](#checklist-for-new-project)
	- [Development language](#development-language)
	- [Scripting language](#scripting-language)
	- [Architecture Style](#architecture-style)
	- [Backend Concerns](#backend-concerns)
	- [Testing Concerns](#testing-concerns)
	- [Operations Concerns](#operations-concerns)
	- [Development Concerns](#development-concerns)
	- [Secruity/Infosec](#secruityinfosec)
	- [Front end concerns](#front-end-concerns)
	- [Links](#links)

## Development language

- Language to use
  - java, c-sharp
- Features of language
  - Does it allow me to meet the technical needs the application should provide
    - embedded systems - c/c++
    - Low memory and fast - c/c++
    - Machine learning - python
    - enterprise/middleware - java/c#
    - etc
  - Maturity
  - Stability
  - Backwards compatibility
  - Community
  - Cross platform
  - Drivers for hardware or databases
  - libraries
    - Specific for usecase of application ie machine learning
    - Stable and Maintained
    - Huge choice
  - Secruity and language patches
  - memory management - manual or automated
  - memory statistics - jmx, jprofile
  - Modularity
  - Concurrency
  - Knowledge of workers, access to workers
  - Can host on equipment
    - Not an issue with docker

[Top of Page](#checklist-for-new-project)

## Scripting language

- bash, python
- make, ansible

[Top of Page](#checklist-for-new-project)

## Architecture Style

- Monolithic
  - Might not support a flexible release cycle but doesn’t need potentially fragile distributed communication.
  - Whole funcitionality can be released at once
- (micro)- services
  - Flexible, only need to deploy ones that changes
  - Smaller, and thus less code to maintain
  - distrubited so communication and infrastructure maintainance an issue
- Style, organisation
  - Clean, mvc, domain driven design, framwork??
  - Event driven (async) or synchronous??
  - Modularising and package structure??
    - Java9? OGCD? Static analysis tools
  - 12 factor app

[Top of Page](#checklist-for-new-project)

## Backend Concerns

- Logic or domain concerns 
- Logging
  - Use SLF4J with either Logback or Log4J2 underneath.
  - How to manage logs
    - files and or console output
    - length of rentention
    - searchable
    - Format and levels (info/error/warn/debug)
    - Which information should be logged when?
- Exception handling
  - Should app go down?
- Application Server
  - WAR that works on a separate server like tomcat/wildfly
    - monolith
  - Embedded server (jetty/spring), the application starts up this server and runs access to the app
    - microservices
    - Docker
- Job Execution
  - What services are needed to be excuted at a regular interval or time
  - ie leaning up a database or batch-importing third-party data
  - quartz for more features
  - spring for basic jobs
- Database Refactoring
  - how to update the structure of your relational database between two versions of your software
    - migrations
    - zero down time migrations
  - In small projects, manual execution of SQL scripts may be acceptable,
  - in medium-to-large projects you may want to use a database refactoring framework like Flyway or Liquibase
- Integrations with internal applications
  - Do we need an adaptor?
- API Technology
  - How will it communicate with other services
  - third party apis
    -  is there a choice? What documentation? Can it be changed on their end?
  - Internal services
    - types of communications
      - http rest, Soap, jms, rpc, files/ftp
    - Contract testing
      - pacts
    - Messeging and queues (Asynchronous communcations)
      - streaming data - kafka
      - message brokers - amq
- API Documentation
  - The internal and external APIs you create must be documented in some form
- Measuring Metrics
  - Are there any metrics like thoughput that should be measured while the application is running?
  - Dropwizard
  - Prometheus Java Client.
  - Use Grafana to hava dashboards of graphics
  - Custom metrics, related to application
- Monitoring
  - metrics
  - status pages
  - application readiness
  - tracing
- Environment configuration
  - dynamic or static properties
  - Secrets
  - puppet
- Authentication
  - How will users of the application prove that they are who they claim to be? Will users be asked to provide username and password or are there additional credentials to check?
  - With a client-side single page app, you need to issue some kind of token like in OAuth or JWT, OpenID
  - In other web apps, a session id cookie may be enough.
  - Use of tls or mutual tls, checking certificates that are signed by trusted
  - Basic Auth
- Authorization
  - how will the application check what the user is allowed to do and what is prohibited?
  - On the server side, Spring Security is a framework that supports implementation of different authorization mechanisms.
- Database Technology
  - Does the application need a structured, schema-based database?
    - Use a relational database.
  - Is it storing document-based structures?
    - Use MongoDB.
  - Key-Value Pairs?
    - Redis.
  - Graphs?
    - Neo4J.
  - Who manages this?
  - Are we stuck on a specific technology
- Data
  - Migrations during deployment
  - retention policy (how long to hold onto)
    - Secruity
    - GDPR
  - Secruity
    - What to encrypt when writing
    - What to return
      - ie Not customer details but a token
    - Who has access? What are they authorised to do?
  - Reporting and dataware house
    - what needs to be stored for long term use?
    - Does there need to be a transfer of data to another tech for other teams to use? Or just expose read only  views?
  - Audits
    - Communication with third parties
    - What to audit?
    - Where to store?
- What available libraries/frameworks that we can use?
  - Open source? Version?
  - Passed secruity check?
  - Do we create our own custom libraries?
  - How to make sure frameworks/libraries are not taking over the app
    - What can be part of the whole app or business logic
- Persistence Layer
  - When using a relational database, Hibernate is the de-facto default technology to map your objects into the database.
  - there are alternative database-accessing technologies like iBatis and jOOQ
  - Spring Data JPA also supports many NoSQL databases like Neo4J or MongoDB.
  - Can use custom access, jdbctemplate or pure jdbc with sql
  - Use sql or orm?
- Caching
  - Cache replacement policies (https://en.wikipedia.org/wiki/Cache_replacement_policies) ??
  -

[Top of Page](#checklist-for-new-project)

## Testing Concerns

- Testing pyramid
- Full end to end integration tests
- Acceptance Tests
  - in memory db or test db on container
  - stubbed out apis or brokers
    - wiremock, trafficparrot
- Unit tests 
  - social tests (start from use case)
    - using fakes (which are tested)
  - individual tests
    - using mocks
- Performance tests
  - SLAs
- Stress tests
- Contract testing
  - use this instead of full integration tests
- Smoke tests
  - automated
  - For deployments into new environments, different clusters
- Production tests
- Environments for testing
  - What dependencies are stubbed by us
  - What dependnecies have a test version that can be used
    - how to setup data, get resources
- Local manual testing 
  - docker
- Documentation from tests
  - Yatspec, cucumber
  - What tests to document
- Test coverage
  - static style - Pitesting
  - line coverage - jacoco
- app integration tests
- Tools
  - Junit, mockito, assertj, hamcrest
  - selenium
- Component testing
  - dockerised app
  - Use of stub app to prime api calls
- Manual testing in different environments
  - provide ways to prime for different test cases (ie gui)
  - code primings 

[Top of Page](#checklist-for-new-project)

## Operations Concerns

- Continuous Delivery
  - Are there automatic tasks that deploy your application to a development, staging or production environment?
  - How will these tasks be executed?
  - Will scripts or configuration files be manually created or automated using minimum info the app needs to run
  - Manual gates
    - A break to ensure the deploying to an environment is though out and everything is ready to go
  - Quality gates
    - fails on status page or smoke tests
- Release process
  - during day or night
  - who needs to be available
    - Expectations
    - Location
    - Equipment
  - Access to servers/db for fixing bugs
  - Rollback strategy
  - Testing strategy
- Servers
  - 	Will the application be hosted on real hardware or on virtual machines?
  - Docker is a popular choice for virtualization nowadays.
- Management of servers and applications
  - Will this be done manually by SAs ?
  - Will be done using kubernetes ?
  - Will it be on the cloud?
- Service Registry
  - When building a (Micro-)Service Architecture, you may need a central registry for your services so that they find each other
  - Service mesh
    - istio, consul
- Database Operations
  - What are the requirements towards the database?
  - Does it need to support hot failover and / or load balancing between database instance?
  - Does it need online backup?
  - What is the deletion process?
- Central Log Server
  - Especially in a distributed architecture with many deployment units, but also in a monolithic application (which also should have at least two instances running), a central log server may make bug hunting easier.
  - The Elastic Stack (Elastic Search, Logstash, Kibana) is popular
- Monitoring
  - How is the health of the server instances monitored and alarmed (Icinga may be a fitting tool)?
  - Who will be alarmed?
  - Should there be a central dashboard where all kinds of metrics like thoughput etc. are measured (Prometheus + Grafana may be the tools of choice).
  - How will be supporting the releases? Timetabling?
- Load Balancing
  - How will the load on the application be balanced between multiple instances of the software?
  - Is there a hardware load balancer?
  - Does it have to support sticky sessions?
  - Does the app need a reverse proxy that routes requests to different deployment units of the application (you may want to use Zuul)?
  - Nginix
- Proxies
- Network Infrastructure
  - How is the network setup?
  - Are there any communication obstacles between different parts of the application or between the application and third party applications?
- Secrets
  - Vault
- Certificates 
  - server
  - client
- Automating environments
  - Terraform
- Expiry dates
  - certifactes, licenses, secrets
  - When do they occur? Is there a reminder/monitor - alerting system, emails etc?
- Gitops 
  - state of deployments stored in git
  - flux 

[Top of Page](#checklist-for-new-project)

## Development Concerns

- IDE
  - What’s the policy on using IDE’s? licence costs
  - Is each developer allowed to use his/her IDE of choice?
  - Making a specific IDE mandatory may reduce costs for providing several parallel solutions while letting each developer use his favorite IDE may reduce training costs.
  - plugins 
    - custom made, free, paid
    - legal usage
  - Mastery, shorcuts 
  - e.g. Intellij, eclipse
- Build Tool
  - Which tool will do the building?
  - Both Maven and Gradle are popular choices
  - Old school is Ant
  - Or do manual using make files and bash scripts
- Version Control
  - Where will the source code be hosted?
    - Gitlabs (internal) or github (external)
  - Secruity
    - access to view and upload/push
    - secrets hidden/encrypted
  - Git is quickly becoming the de-facto standard, but Subversion has a better learning curve.
  - What needs to checked in?
    - Passwords or sensitve data (encrypted or reference local env variables)
  - README.md
    - Standardised for devs to run, test and understand code to be productive
- Coding Conventions
  - How are classes and variables named?
  - Is code and javadoc in english or any other language?
  - choose an existing code formatter and a Checkstyle rule set and include it as a build breaker into the build process
  - Findbugs, PMD for build static analysis tools
  - Sonarcube for hosted analysis tools
- Code Quality
  - How will you measure code quality?
  - Are the coding conventions enough or will you run additional metrics on the code?
  - How will those metrics be made visible?
  - You may want to setup a central code quality server like SonarQube for all to access.
- Application fitness
  - Does it meet the goals of key engineering principles
  - Evolutionary architecture by Ford
  - Tests that check fetures, fitness tests
  - service-level agreement (SLA
  - operational-level agreement (OLA)
- Pairing or/and Code reviews
  - Will you perform code reviews during development?
  - How will thos code reviews be supported by software?
    - github, reviewboard, pairing
  - When will they be performed?
  - How will they be done? 
    - conventions set
  - Metrics used
  - Is there a precheck before review is done 
    - branch build - runs build, static analysis tests
- Pair programming
  - When will this be done?
  - How long for?
    - Monitoring equal pairing
  - Switching up?
  - Styles?
  - Equipment?
    - one box two computers Or laptops
    - Monitors
    - keyboards & mice
    - desks
    - chairs
  - Remote pairing 
    - software? licenses?
- Trunk or feature/branch based development
  - use of feature toggles for trunk based
  - How/when to merge?
  - CI setup, so master in good state
    - build monitor to inform about issues with failng builds
  - Architecture so different stories in play wont affect all or minmal amount of same code being changed
- Continuous Integration
  - How will the build process be executed on a regular basis?
  - There are cloud providers like CircleCI or Travis or you may install a local Jenkins server, teamcity or GoCD.
  - Infrastructure as code for settings for builds
- Build Monitors
  - A screen which displays any failing builds from CI (red builds)
  - Any metrics from Production
  - Calendars/events or reminders
  - Equipment - monitor and box (pc/raspberry pi)
    - location - visable
- CI and CD separated/continous
  - binary from CI is not the same as deployed version
  - Each CI build has continous build to deployment
- Documentation
  - Which parts of the application should be documented how?
  - What information should be documented in a wiki like Confluence?
  - what should be put into Word documents?
  - If there is a chance, use a markup format like Markdown ord AsciiDoc instead of Word.
  - Tests as documents ie acceptance tests
    - Yatspec, cucumber etc
    - Format, wording, diagrams, location, searchable
- Licensing
- Stories
  - Use of jira to track and document stories
  - Breaking down when too long?
  - How to handle TODOs in code?
  - Printing
- Agile
  - kanban or scrum
  - Physical dashboard
    - linked to computer board (jira/trello)
  - retros
  - planning sessions
  - stand ups
- Communication
  - Location
    - colocated
    - remote
      - how to communicate
  - Meeting rooms
  - Accessories
    - whiteboards (large/small)
    - post its
    - notepads
  - Email
    - secure
  - chat/messaging
    - secure

[Top of Page](#checklist-for-new-project)


## Secruity/Infosec

- OWASP
- Code security
  - who can access, who can change
- Deployment security 
  - who can deploy? who can access the pod?
- Data security
- network security 
- Secrets
  - Authentication and authorisation
  - vault
- Sensitive data
- certificates 
- secure communications
- monitoring access
  - who? what did they do? when?

[Top of Page](#checklist-for-new-project)

## Front end concerns

- Frontend Technology
  - Is the application required to be hosted centrally as a web application or should it be a fat client?
  - If a web application, will it be a client-side single page app (use Angular) or static web page
  - if a server-side web framework (I would propose using Apache Wicket or Thymeleaf / Spring MVC over frameworks like JSF or Vaadin, unless you have a very good reason).
  - If a fat client, are the requirements in favor of a Swing or JavaFX-based client or something completely different like Electron?
- Client-side Database
  - Do the clients need to store data?
  - In a web application you can use Local Storage and IndexedDB.
  - In a fat client you can use some small-footprint database like Derby.
- Peripheral Devices
  - Do the clients need access to some kind of peripheral devices like card readers, authentication dongles or any hardware that does external measurements of some sort?
  - In a fat client you may access those devices directly, in a web application you may have to provide a small client app which accesses the devices and makes their data available via a http server on localhost which can be integrated into the web app within the browser.
- Design Framework
  - How will the client app be layouted and designed?
  - In a HTML-based client, you may want to use a framework like Bootstrap.
  - For fat clients, the available technologies may differ drastically.
- Measuring Metrics
  - Are there any events (errors, client version,etc) that the client should report to a central server?
  - How will those events be communicated to the server?
- Offline Mode
  - Are the clients required to work offline?
  - Which use cases should be available offline and which not?
  - How will client side data be synchronized with the server once the client is online?
- CDNs
  - Faster access to resources ie images, music, html etc
- Libraries
  - Secure
  - Maintained with good support
  - Use open source
  - Develop internal libraries

[Top of Page](#checklist-for-new-project)

## Links

- http://adriangrigoras.com/blog/architecture-review-checklist/

[Top of Page](#checklist-for-new-project)
