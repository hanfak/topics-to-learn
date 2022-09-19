# Domain layer patterns
- organising code in the domain layer helps with maintainability
- Clear space to put details of what the application does for its purpose
  - regardless of the technologies used (ie databases, message queues etc)
- Reduce duplication, as it is one place, and should not be recreated elsewhere

## types
### Transaction script
- More procedural
- A single procedure for each action a user can do
  - not all l
  ogic is in this one procedure
-  all biz logic and database logic in a single procedure which may contain sub procedures.
- Useful for straight up database operations like CRUD, with minimal business logic
- Becomes unwieldy as the logic/complexity grows
### domain model
- More OO
- build a model of our domain which is organized around the nouns in our domain
- a noun corresponds to an object, its characteristics are the object properties and what it can do its the object API (public methods)
- handle increasingly complex logic in a well organized and maintainable way
### Table module
- middle ground between Transaction Script and Domain Model.
- Organizes domain logic with one class per table or view or query, and single instance of class contains various procedures to process the data
- usually used with Table Gateway or Record set.
- organizes the domain logic around tables instead of domain objects or straight procedures
- easier to work with Table Module with relational databases.
  - But can tie you down to your database schema
### service layer
-  establishes a set of available operations and coordinates the application's response in each applications.
-  a middle layer which will coordinate interaction between different interfaces and Domain Logic. That will provide encapsulation for your domain logic.
- Split domain layer in two
  - A service layer is placed over an underlying domain model or table module
- The presentation layer interacts solely through the service layer
- Acts as an api for the application
- also known as use cases
- Good place to put transaction control and security
- Can act as a Facade for the lower-level objects, only responsible for forwarding calls and data to them.
### Patterns
- anaemic domain/entity and rich usecase
  - use case contains all behaviour
  - domain are just data objects or data structures
- rich service and  anaemic domain/entity
  - use case contains only workflow behaviour
    - communicating between objects and repository, but no business logic
  - domain services contains all the business logic
  -  domain entities contains only data and no behaviour, generally immutable data structures
  - more functional
- Rich entities
  - use case contains only workflow behaviour
  - domain entity contains all business logic
  - more Object Oriented
- Logic specific in usecase, logic common for mulitple usecases in domain/entities
### Which To Use
- general start with the simplest and refactor to a pattern which is more useful for the application
### model layer
