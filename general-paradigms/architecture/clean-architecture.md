# Clean Architecture


- [Clean Architecture](#clean-architecture)
	- [Aim:](#aim)
	- [Description](#description)
	- [Cost](#cost)
	- [Package structure](#package-structure)
		- [Links](#links)
	- [Use cases and Domain](#use-cases-and-domain)
	- [Incoming Adpaters (infrastructure, web layer)](#incoming-adpaters-infrastructure-web-layer)
	- [Outgoing Adpaters (infrastructure, data layer)](#outgoing-adpaters-infrastructure-data-layer)
	- [Testing Architecture Elements](#testing-architecture-elements)
	- [Mapping Between Boundaries](#mapping-between-boundaries)
	- [Assembling the Application](#assembling-the-application)
	- [Enforcing Architecture Boundaries](#enforcing-architecture-boundaries)
	- [Taking Shortcuts Consciously](#taking-shortcuts-consciously)
	- [Issues](#issues)

Goes by many names
- hexagonal
- ports and adapters
- onion

## Aim:

- the business rules are testable by design and independent of frameworks, databases, UI technologies and other external applications or interfaces
  - domain code must not have any outward facing dependencies.
  - all dependencies point toward the domain code.
- reduce the number of reasons to change throughout the codebase.
  - Less reasons to change means better maintainability.
- Allows for parallel work on same code base
  - one can work on different layers, horizontal slices
  - one can work multiplefeatures, vertical slices
- Easier to test
- Easier to navigate
- Can work on domain and usecase, without worrying about low level details such as databases, as we will be dealing with the interfaces

[Top of Page](#clean-architecture)

## Description

- The core of the architecture contains the domain entities which are accessed by the surrounding use cases.
  - We can model the domain using domain driven design
- The use cases are what we have called services earlier, but are more fine-grained to have a single responsibility
  - Thus no broad services
  - contains ports which adapters in outer layers implements (for DIP)
    - For entrypoints, such a port might be an interface that is implemented by one of the use case classes in the core and called by the adapter.
    -  For a driven adapter, it might be an interface that is implemented by the adapter and called by the core.
- Around this core we can find all the other components of our application that support the business rules.
  - providing persistence or providing a user interface
  - provide adapters to any other third-party component.
  - infrastructure
  - The details, which can be easily changed
  - Adapters
    - input/entry points, drive application, as they call it
    - dataproviders, the applications calls these

## Links

- https://beyondxscratch.com/2017/08/19/hexagonal-architecture-the-practical-guide-for-a-clean-architecture/
- https://jmgarridopaz.github.io/content/hexagonalarchitecture.html
- https://netflixtechblog.com/ready-for-changes-with-hexagonal-architecture-b315ec967749
- https://alistair.cockburn.us/hexagonal-architecture/
- https://blog.cleancoder.com/uncle-bob/2012/08/13/the-clean-architecture.html
- http://geekswithblogs.net/cyoung/archive/2014/12/20/hexagonal-architecturendashthe-great-reconciler.aspx
- https://jeffreypalermo.com/2008/07/the-onion-architecture-part-1/

## Examples

- https://gitlab.com/crafts-records/talkadvisor/talkadvisor-back
- https://github.com/jmgarridopaz/bluezone
- https://github.com/mattia-battiston/clean-architecture-example

[Top of Page](#clean-architecture)

## Cost

- we have to maintain a model of our application’s entities in each of the layers.
  - that means we have to translate between both representations when the domain layer sends and receives data to and from the persistence layer. The same translation applies between the domain layer and other outer layers.
  - This is good as we are decoupling
  -

[Top of Page](#clean-architecture)

## Package structure

- Help organise code
- Having an expressive package structure, which screams the intent of the applicaiton and it's services
- Generally set up at the beginning of the project ie greenfield
  - but need to maintain it, and not just be a facade with chaos underneath
- The aim is to bridge the gap between fight against the so-called “architecture/code gap” or “model/code gap”
  - Need a better mapping, so that it is easier to discuss
- The expressiveness of the structure, means we have to think carefully about where to put our classes
- Downside, everything has to be public, cannot rely on compiler to help maintain package structure
- infrastructure/adapter package, we can swap out different implementations as long as they use the same interface
  - This allows us to store use of libraries or frameworks in this package, and pollute the domain logic with it, thus keeping domain/usecase independent
- Use of dependency injection
  -  incoming adapters, like a web adapter, tsince the control flow points in the same direction as the dependency between adapter and domain code. The adapter simply calls the service within the application layer.
    - In order to clearly demarcate the entry points to our application, we might want to hide the actual services between port interfaces nonetheless.
  - For outgoing adapters, like our persistence adapter, we have to make use of the Dependency Inversion Principle to turn the dependency against the direction of the control flow.

### Example

```
1 Application
2 └──account
3     ├── adapter
4     |   ├──in
5     |   |  └── web
6     |   |      └── AccountController
7     |   ├──out
8     |   |  └── persistence
9     |   |       ├── AccountPersistenceAdapter
10    |   |       └── SpringDataAccountRepository
11    ├── domain
12    |   ├── Account
13    |   └── Activity
14    └── application
15    |   └── SendMoneyService
16    |   └── port
17    |       ├── in
18    |       |   └── SendMoneyUseCase (I)
19    |       └── out
20    |           ├── LoadAccountPort (I)
21    |           └── UpdateAccountStatePort (I)
22    └── wiring
23
```

- Each element of the architecture can directly be mapped to one of the packages.
- A package named account, indicating that this is the module implementing the use cases around an Account.
  - Can multiple modules, which contain multiple services
  - This can be only one module, ie microservices
- The domain package containing our domain model.
- The application package contains a service layer around this domain model
  - The SendMoneyService implements the incoming port interface SendMoneyUseCase and
  - uses the outgoing port interfaces LoadAccountPort and UpdateAccountStatePort, which are implemented by the persistence adapter.
  - Instead of having packages for ports in and out, can just have packages for each service and include the interfaces for adapters in here
  - Aim is for this layer  not to have dependencies to the incoming and outgoing adapters
- The adapter (aka infrastructure) package contains
  - the incoming adapters that call the application layers’ incoming ports
    - Multiple packages ie web, jms, commandline, scheduler etc
  - the outgoing adapters that provide implementations for the application layers’ outgoing ports.
    - Multiple packages ie http clients, persistence, files
  - Include other low level details not associated with domain logic
    - ie logging, properties, status/health checks, metrics, unmarshalling/marshalling etc
  - We can also avoid using using subpackages for in and out, and just put everthing in an infrastructure package
- Wiring wraps the whole app
  - news everything up
  - Dependency to all layers
  - Can use a DI framework
  - Must know everything about all classes in all the packages which needs to be instantiated
  - The main method lives here to start the application
- Having multiple modules, ie Account, maps directly to domain driven design and bounded contexts

[Top of Page](#clean-architecture)


### Links

- https://codeforfunandmoney.wordpress.com/2016/07/13/domain-driven-design-and-package-organization/
- http://tomhesl.in/package-structure-in-a-domain-driven-design-project/

## Use cases and Domain

- As application/domain layer is independent, we can model the domain using
  - Domain driven design
  - anemic domain models
  - rich domain models
  - other
- Implementing a Domain model
  - this is the types/entities that are used in the use case
  - The entity can have behaviour - rich domain models
  - Domain types, only have state
- A usecase does
  - Take input
  - Validate business rules
  - Manipulate model state
  - Return output
- use case takes input from an incoming adapter
- use case code should care about the domain logic and we shouldn’t pollute it with input validation.
  - Validate business rules,
    - domain objects should also do validation
  - Can put validation in the argument that we send from the input adapter (web server) to the usecase
    - This argument is part of the incoming port package
      - part of usecase adapter interface
      - Thus part of application layer, but not in use case code
  - Can use validation frameworks for simple/common validations ie https://beanvalidation.org/
  - Creates an anti corruption layer around the use case
  - Using a constructor instead of builder
    - this helps check validation at compile time for a new field in input entity
  - Have different input models from the incoming adapter for each different use case
    - Bad to have the same, as we will have fields used for one usecase and not the other, hard to do validation
      - need to allow nulls - code smell
      - Will need complex validation logic
    - A dedicated input model for each use case makes the use case much clearer and also decouples it from other use cases, preventing unwanted side effects.
    - All this mapping has a cost
  - input validation is a syntactical validation, while a business rule is a semantical validation in the context of a use case.
  - Validating business rules
    - core of application
    - validating a business rule requires access to the current state of the domain model while validating input does not
    - Can put business rules in the domain entity
      - easy to locate and reason about
    - Can also put it in the use case code,
      - it might need info from outgoing ports ie database etc, to do the validation
      - if validation fails can throw a dedicated exception, which is handled in the web adapter or just given to user and they handle it
- If the business rules were satisfied, the use case then manipulates the state of the model in one way or another, based on the input
  - Applies business rules
  - it usually changes the state of a domain object (or create new object with new state) and pass this new state to a port implemented by the persistence adapter to be persisted
  - it can also call other outgoing adapters such as 3rd party api, files etc
  - These can happen in different order
- Last step, is for use case to translate the return value from the outgoing adapter into an output object which will be returned to the calling adapter.
- Aim is to
  - create a separate service class for each use case instead of putting all use cases into a single service class.
- How to implement domain model
  - rich domain model, follows domain driven design
  - rich domain model
    - as much of the domain logic as possible is implemented within the entities at the core of the application.
    - The entities provide methods to change state and only allow changes that are valid according to the business rules.
    - In this model the use case serves as an entry point to the domain model
    - A use case then only represents the intent of the user and translates it into orchestrated method calls to the domain entities which do the actual work.
    - Many of the business rules are located in the entities instead of the use case implementation.
  -  “anemic” domain model
    - the entities themselves are very thin.
    - They usually only provide fields to hold the state and getter and setter methods to read and change it.
    - They don’t contain any domain logic.
    - domain logic is implemented in the use case classes.
    - They are responsible to validate business rules, to change the state of the entities and pass them into the outgoing ports responsible for storing them in the database.
    - The “richness” is contained within the use cases instead of the entities.
- Different Output Models for Different Use Cases
  - the output is as specific to the use case as possible.
  - The output should only include the data that is really needed for the caller to work.
    - ie what the web adapter will use
  - Example should we return boolean to verify something was done (or even void) OR return the updated info? Or should this updated info be in another use case?
    - All depends on the user/caller of app wants
  - When in doubt, return as little as possible.
  - Sharing the same output model between use cases also tends to tightly couple those use cases
    - Applying the Single Responsibility Principle and keeping models separated helps decoupling use cases.
  - we might want to resist the temptation to use our domain entities as output model
    - To keep SRP and improve decoupling
    - We don’t want our domain entities to change for more reasons than necessary
- Read only use cases
  - Such as querying a data provider and no change of state of the application
  - There is little business logic here, only get data
  -  if it’s not considered a use case in the context of the project, we can implement it as a query to set it apart from the real use cases.
  - create a dedicated incoming port for the query and implement it in a “query service”
  - Can have an incoming port interface called XXXquery, which the service in the application layer implements.
    - This way we clearly distinguish services which are usecases (modifying state and applying business rules) from queries (data retrival)
  - We also seperate out outgoing ports for dataproviders into queries and commands
  - Allows application to follow CQRS
  - We can take a shortcut, by allowing the incoming adapter directly call the outgoing port for the data provider and skip the call via the service
    - This can be a slippery slope, if not thinking about it
    - ie business rules can end up in incoming adapters

[Top of Page](#clean-architecture)

## Incoming Adpaters (infrastructure, web layer)

- Most applications today have some kind of web interface
  - either a UI that we can interact with via web browser or
  - an HTTP API that other systems can call to interact with our application.
- In this architecture, all communication with the outside world goes through adapters
- A web adpater acts as a controller
  - which calls a port in interface implemented by a service in the application layer
  - Using DIP
  - We can just let the web adapter directly callt he service without using DIP, as the flow is natural for clean Architecture
    - This is a short cut ?????
  - why have this incoming port for the service?
    - the ports are a specification of the places where the outside world can interact with our application core.
    - Having ports in place, we know exactly which communication with the outside world takes place
    - Helps with maintance
  - For using realtime data and websockets, can use this layer
    - It will use an incoming port and outgoing port from the service
      - These ports can be the same
- Responsibilities of web adapter
  - Consists of
    - Map HTTP request to Java objects
    - Perform authorization checks
    - Validate input
    - Map input to the input model of the use case
    - Call the use case
    - Map output of the use case back to HTTP
    - Return HTTP response
  - The web adapter must listen to HTTP requests that match certain criteria like a certain URL path, HTTP method and content type
    - A controller, using a server like Jetty
  - a web adapter then does an authentication and authorization check and returns an error if it fails.
    - Checks whether use can access this end point
    - Tokens, certs, login etc
  - The parameters and the content of a matching HTTP request must then be deserialized into objects we can work with
    - Unmarshalling into objects that can be used by the system
      - ie turning json/xml into objects
      - Does validation on input and returns error if input is not matching or malformed json/xml
        - Can we transform http request into input model of web adpater?
        - This validation is different to input validation for use case
        - Should be different validation
  - To call a certain use case with the transformed input model. The adapter then takes the output of the use case and serializes (marshalls) it into an HTTP response which is sent back to the caller.
  - If anything goes wrong on the way and an exception is thrown, the web adapter must translate the error into a message that is sent back to the caller.
    - Instead of using exceptions to drive flow, and not letting use see stack traces (which are shown in logs)
    - Can use return types from service that include multple values ie success or fail (ie with error code and error description), which gets rendered as http response
  - Anything to do with HTTP must not leak into the application layer.
    - If the application core knows that we’re dealing with HTTP on the outside, we have essentially lost the option to perform the same domain logic from other incoming adapters that do not use HTTP.
    - **This happens naturally if we start programming from the domain/app layer instead of the web layer**
- Slicing controllers
  - Many controllers that handles one input into app or one controller that handles many inputs into app?
    - Stick to building many controllers or servlets
  - each controller implements a slice of the web adapter that is as narrow as possible and that shares as little as possible with other controllers.
  - By creating one controller for many services
    - We have big classes, which means big test classes
    - putting all operations into a single controller class encourages re-use of data structures
      - Meaning fields can be null for some endpoints, validation becomes complex
    - What about some request which cannot be put into a simple general controller, as it needs more info
  - **Should create a separate controller, potentially in a separate package, for each operation. Also, we should name the methods and classes as close to our use cases as possible**
  - **each controller can have its own model or use primitives**
    - From paramters of url, can map to primitives, which map to input model of usecase
    - From json, can unmarshall to web adapter model for controller, then map to input model of usecase
    - These controller input models can be private in class, or package private in same package
      - so not reused else where
    - Controllers may still share models, but using shared classes from another package makes us think about it more and perhaps we find out that we don’t need half of the fields and create our own, after all.
  - Should have desciptive rich names for controllers, models etc

[Top of Page](#clean-architecture)

## Outgoing Adpaters (infrastructure, data layer)

- In clean architecture, the data/persistence layer is not the main dependency of application. It becomes a detail which we can swap out due to DIP.
- data/persistence provider does not just mean talk to database or datastore
  - it can also mean talk via http to another service to handle data operations or perform some services
  - it can also mean sending messages via message queues
- A data/persistence layer is just a persistence adapter that provides persistence functionality to the application services
  - where we can replace the adapter whenever it suits us
- persistence adapter class that does the actual persistence work and is responsible for talking to the database
- The service will talk to the outgoing port interface, which is implemented by the persistence adapter
  - The service then has no idea about the implementation and is not coupled with it
- We need the outgoing port for the service to talk to, maintain the flow of dependencies during compile time
  - At runtime, ie wiring and instantiation, we still have a dependency from our application core to the persistence adapter.
- Responsibilities of a Persistence Adapter
  - Consists of:
    - Take input
    - Map input into data provider format
    - Send input to the data provider or ask for data from provider
    - Map data provider  output into application format
    - Return output
  - persistence adapter takes input through a port interface.
    - The input model may be
      - a domain entity or
      - an object dedicated to a specific database operation, as specified by the interface.
  - From input model going into persistence adapter, it maps the input model to a format it can work with to modify or query the dataprovider
    - ie using JPA or plain sql for database operations
    - ie using request object for http operations
  - the input model to the persistence adapter lies within the application core and not within the persistence adapter itself
    - so that changes in the persistence adapter don’t affect the core.
  - the persistence adapter queries/modifies/request the dataprovider and receives the results.
  - it maps the data provider's answer into the output model expected by the outgoign port and returns it.
    - he output model lies within the application core and not within the persistence adapter.
- Slicing Port Interfaces
  - It’s common practice to create a single repository interface that provides all database operations for a certain entity
    - the outgoing port interface is very broad
    - who ever uses this interface may not use all the methods inthe interface
    - This means we have unnecessary dependencies in our codebase. Harder to test and understand
  - **Depending on something that carries baggage that you don’t need can cause you troubles that you didn’t expect.**
  - **The Interface Segregation Principle provides an answer to this problem. It states that broad interfaces should be split into specific ones so that clients only know the methods they need.**
    - Instead split the interfaces into many that the adapter implements
    - Naming of the interfaces becoming richer
  - “one method per port” approach may not be applicable in all circumstances.
    - There may be groups of database operations that are so cohesive and often used together that we may want to bundle them together in a single interface.
- Slicing Persistence Adapters
  - We can create multiple persistance adapter classes
  - ie implement one persistence adapter per domain class for which we need persistence operations (or “aggregate” in DDD lingo)
    - our persistence adapters are automatically sliced along the seams of the domain that we support with persistence functionality.
  - Can split them up to use different implementations
    - ie one set uses JPA another set uses sql
  - The “one persistence adapter per aggregate” approach is also a good foundation for separating the persistence needs for multiple bounded contexts in the future
    - The term “bounded context” implies boundaries,
    - ie which means that services of the account context may not access persistence adapters of the billing context and vice versa. If one context needs something of the other, it can access it via a dedicated incoming port.
  - All models should be
    - immutable
    - use static factory methods
    - perform validation before doing creation of new objects when mutating
- Using frameworks for dataproviders (ie hibernate, jpa) can lead to input models being populated with annotations, fields, constructor which is only used for that framework rather than the app
  - this is alright if mapping incoming model to a persistance model used by the adapter
  - but should not contaminate the domain/application entities
- Database transactions
  - A transaction should span all write operations to the database that are performed within a certain use case so that all those operations can be rolled back together if one of them fails.
  - Since the persistence adapter doesn’t know which other database operations are part of the same use case, it cannot decide when to open and close a transaction. We have to delegate this responsibility to the services that orchestrate the calls to the persistence adapter.
  - With Spring can use annotations
  - Can use event sourcing, to allow for rollbacks to an event if there was an issue with an event
  - Can use workflows if something goes wrong with an event, then the failed event is written and can be dealt with by support
  - Use aspect oriented programming

[Top of Page](#clean-architecture)

## Testing Architecture Elements

[Top of Page](#clean-architecture)

## Mapping Between Boundaries

- Need to make decisions about whether to use the same models in two or more layers
  - If we don’t map between layers, we have to use the same model in both layers which means that the layers will be tightly coupled!
  - if we do map between layers, we produce a lot of boilerplate code which is overkill for many use cases, since they’re only doing CRUD and have the same model across layers anyways!
- With incoming and outgoing ports acting as gatekeepers between the layers of our application,
  - define how layers communicate
- With narrow ports in place for each use case, we can choose different mapping strategies for different use cases, and even evolve them over time without affecting other use cases, thus selecting the best strategy for a certain situation at a certain time.
- We can always change the mapping strategies as the app evolves
- No mapping strategy should be considered an iron law
- No mapping strategy
  - Using the same models through out layers
  - Example, Account model object is passed from web adapter to usecase incoming port, thus used by applicaiton layer service. The service calls outgoing port and passes the account object to it. The outgoing adapter ie database, returns the account object back to the service. etc etc
  - Consequences
    - the other layers may have special requiremetns for their models
    - Use of annotations or empty constructors
    - Extra fields only used in another layer
    - This means the domain model will have stuff it does not need
      - breaks SRP, as domain model will need to change if web or database changes
  - A good use wood be CRUD applications
  - **As long as all layers need exactly the same information in exactly the same structure, a “no mapping” strategy is a perfectly valid option.**
  - When not to use
    - **As soon as we’re dealing with web or persistence issues in the application or domain layer (aside from annotations, perhaps), however, we should move to another mapping strategy.**
- The “Two-Way” Mapping Strategy
  - A mapping strategy where each layer has its own model is what I call the “Two-Way” mapping strategy
  - Each layer has its own model, which may have a structure that is completely different from the domain model.
  - The web layer maps the web model into the input model that is expected by the incoming ports. It also maps domain objects returned by the incoming ports back into the web model.
    - same for other layers
  - each layer can modify its own model without affecting the other layers (as long as the contents are unchanged)
    - The web model can have a structure that allows for optimal presentation of the data.
    - The domain model can have a structure that best allows for implementing the use cases.
    - the persistence model can have the structure needed by an OR-Mapper for persisting objects to a database.
  - this leads to a clean domain model that is not dirtied by web or persistence concerns. It does not contain JSON or ORM mapping annotations
  - The mapping responsibilities are clear: the outer layers / adapters map into the model of the inner layers and back.
    - The inner layers only know their own model and can concentrate on the domain logic instead of mapping.
  - Consequence
    - a lot of boilerplate code
    - implementing the mapping between models usually takes up a good portion of our time
    - debugging mapping logic is a pain - especially when using a mapping framework that hides its inner workings behind a layer of generic code and reflection.
    - the domain model is used to communicate across layer boundaries.
      - The incoming ports and outgoing ports use domain objects as input parameters and return values.
      - This makes them vulnerable to changes that are triggered by the needs of the outer layers whereas it’s desirable for the domain model only to evolve due to the needs of the domain logic.
- The “Full” Mapping Strategy
  - has a separate input and output model per operation
  - Instead of using the domain model to communicate across layer boundaries,
    - we use a model specific to each operation, like the DoSomethingCommand, which acts as an input model to the DoSomethingUseCase port in the figure.
    - We can call those models “commands”, “requests”,
  - The web layer is responsible for mapping its input into the command object of the application layer.
    - Such a command makes the interface to the application layer very explicit
    - Each use case has its own command with its own fields and validations
  - The application layer is then responsible for mapping the command object into whatever it needs to modify the domain model according to the use case.
  - Consequence
    - lots of mapping code
  - this mapping, however, is significantly easier to implement and maintain than a mapping that has to handle the needs of many use cases instead of only one.
  - it plays out its advantages best between the web layer (or any other incoming adapter) and the application layer to clearly demarcate the state-modifying use cases of the application.
    - I would not use it between application and persistence layer due to the mapping overhead.
  - **I would restrict this kind of mapping to the input model of operations and simply use a domain object as the output model.**
- The “One-Way” Mapping Strategy
  - the models in all layers implement the same interface that encapsulates the state of the domain model by providing getter methods on the relevant attributes.
  - The domain model itself can implement a rich behavior, which we can access from our services within the application layer.
  -  If we want to pass a domain object to the outer layers, we can do so without mapping, since the domain object implements the state interface expected by the incoming and outgoing ports.
  - The outer layers can then decide if they can work with the interface or if they need to map it into their own model
    - They cannot inadvertently modify the state of the domain object since the modifying behavior is not exposed by the state interface.
  - Objects we pass from an outer layer into the application layer also implement this state interface.
    - The application layer then has to map it into the real domain model in order to get access to its behavior.
  - This mapping plays well with the DDD concept of a factory.
    - A factory in terms of DDD is responsible for reconstituting a domain object from a certain state, which is exactly what we’re doing.
  - if a layer receives an object from another layer, we map it into something the layer can work with.
    -  Thus, each layer only maps one way, making this the “One-Way” mapping strategy.
  - Good for
    -  if the models across the layers are similar. For read- only operations, for instance, the web layer then might not need to map into its own model at all, since the state interface provides all the information it needs.
- When to use which Mapping Strategy?
  - we need to agree upon a set of guidelines within the team
    -  which mapping strategy should be the first choice in which situation.
    - They should also answer why they are first choice so that we’re able to evaluate if those reasons still apply after some time.
    - we might want to use different mapping strategies between the web and application layer and between the application and persistence layer.
    - If we’re working on a modifying use case, the “full mapping” strategy is the first choice between the web and application layer, in order to decouple the use cases from one another.
      - This gives us clear per-use-case validation rules and we don’t have to deal with fields we don’t need in a certain use case.
  - If we’re working on a modifying use case, the “no mapping” strategy is the first choice between the application and persistence layer in order to be able to quickly evolve the code without mapping overhead
  - As soon as we have to deal with persistence issues in the application layer, however, we move to a “two-way” mapping strategy to keep persistence issues in the persistence layer.
  - If we’re working on a query, the “no mapping” strategy is the first choice between the web and application layer and between the application and persistence layer in order to be able to quickly evolve the code without mapping overhead
  - As soon as we have to deal with web or persistence issues in the application layer, however, we move to a “two-way” mapping strategy between the web and application layer or the application layer and persistence layer, respectively.

[Top of Page](#clean-architecture)

## Assembling the Application

- The application wont work, unless we instantiate all the classes that do the work
- This happens at start up, when the main method is called.
- Called wiring or configuration
    - it is just a bunch of factories
- Use Dependency Injection framework or you can new up the classes manually
- We dont want to instantiate the dependencies in the classes
  - Because we want to keep the code dependencies pointed in the right direction.
  - coupling
  - better to test
- must be a configuration component that is neutral to our architecture and that has a dependency to all classes in order to instantiate them
- This wiring layer is the outer most layer
- responsible for assembling a working application from the parts we provided. It must
  - create web adapter instances,
  - ensure that HTTP requests are actually routed to the web adapters,
  - create use case instances,
  - provide web adapters with use case instances
  - create persistence adapter instances,
  - provide use cases with persistence adapter instances,
  - and ensure that the persistence adapters can actually access the database.
- the configuration component should be able to access certain sources of configuration parameters, like configuration files or command line parameters
- During application assembly, the configuration component then passes these parameters on to the application components to control behavior like which database to access or which server to use for sending email.
- This does break SRP
  - but we accept this to keep application clean
- Manual wiring
  - This can grow massively
  - since we’re instantiating all classes ourselves from outside of their packages, those classes all need to be public
    - The compiler does not stop one layer using another properly
  - Keeps it easy to understand
- DI framework using class path scanning
  - Spring goes through all classes that are available in the classpath and searches for classes that are annotated with the @Component annotation. The framework then creates an object from each of these classes. The classes should have a constructor that take all required fields as an argument
  - Spring will find this constructor and search for @Component-annotated classes of the required argu- ment types and instantiate them in a similar manner to add them to the application context. Once all required objects are available, it will finally call the constructor of the class and add the resulting object to the application context as well.
  - Drawbacks
    - it’s invasive in that it requires us to put a framework-specific annotation to our classes.
      - If you’re a Clean Architecture hardliner, you’d say that this is forbidden as it binds our code to a specific framework.
    - A lot of magic happens, hard to debug when things go wrong  or understand when the unexpected happens unless you are an expert in this framework
-  Spring’s Java Config
  - we create configuration classes, each responsible for constructing a set of beans that are to be added to the application context.
  - The @Configuration annotation marks this class as a configuration class to be picked up by Spring’s classpath scanning
  - The beans themselves are created within the @Bean-annotated factory methods of our configuration classes.
  - we could create configuration classes for web adapters, or for certain modules within our application layer. We can now create an application context that contains certain modules, but mocks the beans of other modules, which gives us great flexibility in tests
  - We could even push the code of each of those modules into its own codebase, its own package, or its own JAR file without much refactoring.
  - Drawbacks
    - If the configuration class is not within the same package as the classes of the beans it creates (the persistence adapter classes in this case), those classes must be public.
      - To restrict visibility, we can use packages as module boundaries and create a dedicated configuration class within each package. This way, we cannot use sub-packages,

[Top of Page](#clean-architecture)

## Enforcing Architecture Boundaries

- Over time architecture erodes
  - Boundaries between layers weaken
  - code becomes harder to test
  - we generally need more and more time to implement new features
- Need to fight this erosion by enforcing the architecture and it's boundaries
  - Make sure there are no illegal dependencies ie dependencies point in the wrong way
- Visibility modifiers
  - 4 types (public, protected, package private, private)
  - Use package private (default)
    - it allows us to use Java packages to group classes into cohesive “modules”.
    - Classes within such a module that can access each other, but cannot be accessed from outside of the package.
  - We can then choose to make specific classes public to act as entry points to the module
  - The classes in the outgoing adapters/infrastructure (ie database) can be packagae private
    - as accessed by the outgoing port interface
  - the domain package needs to be accessible by the other layers
  - This only works with frameworks, as it uses reflection
  - The package-private modifier is awesome for small modules with no more than a couple handful of classes
    - it grows confusing to have so many classes in the same package.
    - Having subpackages, will fail this mechanism
      - members in sub-packages must be public
- Post-Compile Checks
  - Checks conducted at runtime
  - Such runtime checks are best run during automated tests within a continuous integration build.
  - Use some framework, ie Arhcunit, to check dependencies work, as part of a unit test
  - Drawbacks
    - if we misspell the package name buckpal in the code example above, for example, the test will find no classes and thus no dependency violations
- Build Artifacts
  - Modularising our application
  - Use of maven/gradle
    - A main feature of build tools is dependency resolution
    - To transform a certain codebase into a build artifact, a build tool first checks if all artifacts the codebase depends on are available.
    - If not, it tries to load them from an artifact repository.
    - If this fails, the build will fail with an error, before even trying to compile the code.
  - For each such module or layer, we create a separate build module with its own codebase and its own build artifact (JAR file) as a result.
  - In the build script of each module, we specify only those dependencies to other modules that are allowed according to our architecture.
  - Developers can no longer inadvertently create illegal dependencies because the classes are not even available on the classpath and they would run into compile errors.
  - Can split each layer
  - Can split each package in the layer in to jars/modules
    - ie one module per adapter
      - we usually don’t want changes in the persistence layer to leak into the web layer and vice versa
      - We don’t want details of that API leaking into other adapters by adding accidental dependencies between adapters.
    - ie one module per port
      - Make it clear which is an incoming and outgoing port
    - domain layer as module
      - Depends on whether these will be used in different layers
      - mapping strategy - disallow no mapping strategy if domain is module
      - Can split domain layer packages into modules, and allow for different mapping strategies for specific domain entities
    - services as module
    - wiring as module
  -  **The gist is that the finer we cut our modules, the stronger we can control dependencies between them. The finer we cut, however, the more mapping we have to do between those modules**
  - added cost of having to maintain a build script
  - Advantages
    -  build tools absolutely hate circular dependencies, violates SRP, and dont allow it
    -  build modules allow isolated code changes within certain modules without having to take the other modules into consideration
      - ie we do a major refactoring in the application layer that causes temporary compile errors in a certain adapter.
        - If the adapters and application layer are within the same build module, most IDEs will insist that all compile errors in the adapters must be fixed before we can run the tests in the application layer, even though the tests don’t need the adapters to compile.
        - If the application layer is in its own build module, however, the IDE won’t care about the adapters at the moment, and we could run the application layer tests at will.
      -  multiple build modules allow isolated changes in each module.
        - Can put each module into its own code repository, allowing different teams to maintain different modules.
  - Now we have to thinks about our architecture

[Top of Page](#clean-architecture)

## Taking Shortcuts Consciously

- Taking shortcuts can lead to technical debt
- Need to identify such shortcuts and be able to discuss their effects when deciding to choose to do them or fix them
- Shortcuts are like broken windows
  - if devs see shortcuts, they will automatically use them or copy them in any new features with out thinking about the consequences
  - Broken window theory applied to code
    -  When working on a low-quality codebase, the threshold to add more low-quality code is low.
    -  When working on a codebase with a lot of coding violations, the threshold to add another coding violation is low.
    -  When working on a codebase with a lot of shortcuts, the threshold to add another shortcut is low.
- Need to keep code as clean as possible, so others will treat in the same way
- Why take a shortcut
  - the part of the code we’re working on is not that important to the project as a whole
  - that we’re prototyping
  - for economical reasons
- Should document are architectural decisions, ie Architecture Decision Records (ADRs),
  - If every member of the team is aware of this documentation, it will even reduce the Broken Windows effect, because the team will know that the shortcuts have been taken consciously and for good reason.
- Sharing models between use cases
  - different use cases should have a different input and output model, meaning that the types of the input parameters and the types of the return values should be different.
    - Multiple use cases using the same input/output model, means they are coupled to each other
    - They share a reason to change in terms of the Single Responsibility Principle
    - This can lead to duplicate code, but allows use cases to be decoupled and grow indepdently
  - Sharing input and output models between use cases is valid if the use cases are functionally bound
    - i.e. if they share a certain requirement.
    - In this case, we actually want both use cases to be affected if we change a certain detail.
  - to regularly ask the question whether the use cases should evolve separately from each other.
    - As soon as the answer becomes a “yes”, it’s time to separate the input and output models.
- Using Domain Entities as Input or Output Model
  - incoming/outgoing port has a dependency to the domain entity
  - If the use case needs something from input model which is not in domain entity, then we might be tempted to add a field to the domain entity because it is available
  - For simple create or update use cases, a domain entity in the use case interface may be fine, since the entity contains exactly the information we need to persist its state in the database.
  - As soon as a use case is not simply about updating a couple of fields in the database, but instead implements more complex domain logic (potentially delegating part of the domain logic to a rich domain entity)
    - we should use a dedicated input and output model for the use case interface
    - because we don’t want changes in the use case to propagate to the domain entity
- Skipping Incoming Ports
  - we don’t need the incoming ports for dependency inversion.
    - We could decide to let the incoming adapters access our application services directly, without incoming ports in between
  - The incoming ports, however, define the entry points into out application core
    - Once we remove them, we must know more about the internals of our application to find out which service method we can call to implement a certain use case.
    - By maintaining dedicated incoming ports, we can identify the entry points to the application at a glance.
    - increases readabilitykeep the incoming ports is that they allow us to easily enforce architecture.
  - keeping the incoming ports is that they allow us to easily enforce architecture.
    - we can make certain that incoming adapters only call incoming ports and not application services.
    - No accidental calls of services not meant for the incoming adapter
  - If an application is small enough or only has a single incoming adapter so that we can grasp the whole control flow without the help of incoming ports, we might want to do without incoming ports
- Skipping Application Services
  - we might want to skip the application layer as a whole
  - do this for simple CRUD use cases, since in this case an application service usually only forwards a create, update or delete request to the persistence adapter, without adding any domain logic.
    - Instead of forwarding, we can let the persistence adapter implement the use case directly.
    - requires a shared model between the incoming adapter and the outgoing adapter,
  - we no longer have a representation of the use case within our application core
    - If CRUD app grows, then we start to add domain logic directly to the outgoing adapter. Spreading the domain logic all over the app
    - to prevent boilerplate pass-through services, we might choose to skip the application services for simple CRUD use cases after all
    - Should introduce application service as soon business logic occurs


[Top of Page](#clean-architecture)

## issues

- https://javadevguy.wordpress.com/2017/07/27/a-detailed-analysis-of-the-clean-architecture-from-an-object-oriented-perspective/
- https://www.jamesmichaelhickey.com/clean-architecture/
- https://jimmybogard.com/vertical-slice-architecture/
- https://stackoverflow.com/questions/29576344/drawbacks-of-hexagonal-architecture#:~:text=Since%20Hexagonal%20makes%20use%20of,the%20drawbacks%20of%20those%20patterns%3A&text=Adapters%20are%20traditionally%20polymorphic%20(in,are%20also%20a%20hidden%20indirection).

### Duplication of models

- this approach sometimes requires duplicated entity objects. For example, if a dependent API uses gRPC, you’ll likely already have generated classes representing the entities. But in order to keep business logic protobuf agnostic, you’d have to define your own entity classes that more or less duplicate the protobuf messages
	- solution
		- You would have separate classes yes. The way to think about this is that the classes generated from the protobuf form part of the gRPC client, and are used to represent requests and responses from the gRPC call (part of the infrastructure layer) where as the business layer contains it’s own data representations that make sense in the context of the business logic
		- These will contain similar data, but are conceptually different.
		- So you might have the following defined in your business layer:
		```java
		class User(val username: String, val dateOfBirth: Date)

		interface UserRepository { fun getUsers(): List<User>} // a ‘port’
		```
		- and have the following defined in the infrastructure:
		```java
		class GRPCUser( val email: String, val password: String, val dob: Date ) // Generated from protobuf
		class UserRepositoryGRPC implements UserRepository { … } // an ‘adaptor’
		```
		- It is the responsibility of the adaptor to translate between the two. This as you say, allows the business layer to remain agnostic of how it’s ports are implemented in the infrastructure layer
-  If you share an Entity between all layers then all layers will be effected directly by changes within that Entity.
	- So once you have a model for each layer then you'll also need a mapper for each model, and don't forget the unit tests.
	- you need decide whether you want a scalable, maintainable architecture in cost of extra code
	- To avoid mapping too much, you can use the entities in the core/hexagon, throughout the code base. But models used the outer layers must be mapped to the core entities (to avoid leaking infrastructure technology ie jpa/jackson annotations)

### A higher level of complexity

- Building an application with multiple layers of abstraction will mean that the level of complexity will dramatically increase
	- the on-boarding process for new developers to get a handle on the architecture of the application can be longer
- Premature building of layers, abstraction can make code harder to understand, and cost of time

### The cost of indirection and isolation

- when you have many layers of indirection and isolation, the cost of building and maintaining the application can often be more costly than the benefits of the abstraction.
- optimising for isolation and indirection to make testing your application easier can have a detrimental effect on the design of your application.

### Most web applications don’t need that level of complexity

- Only useful for implementing business logic and need for adaptability
- Most web apps are fixed in terms of frameworks or datasources
- Some are just CRUD apps, and dont need any business logic

[Top of Page](#clean-architecture)

https://github.com/lievendoclo/cleanarch
