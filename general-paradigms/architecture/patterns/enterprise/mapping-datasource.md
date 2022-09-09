# Mapping to datasource
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Mapping to datasource](#mapping-to-datasource)
	- [Good design](#good-design)
	- [Architectural patterns](#architectural-patterns)
		- [Active Record](#active-record)
		- [Gateway](#gateway)
		- [Data Mapper](#data-mapper)
	- [Object-Relational Behavioural Patterns](#object-relational-behavioural-patterns)
		- [Unit of work](#unit-of-work)
		- [Identity Map](#identity-map)
		- [Lazy Loading](#lazy-loading)
		- [Reading Data](#reading-data)
	- [Object-Relational Structural Patterns](#object-relational-structural-patterns)
		- [Identity Field](#identity-field)
		- [Foreign Key Mapping](#foreign-key-mapping)
		- [Association Table Mapping](#association-table-mapping)
		- [Dependent Mapping](#dependent-mapping)
		- [Embedded Value](#embedded-value)
		- [Serialized LOB](#serialized-lob)
		- [Single Table Inheritance](#single-table-inheritance)
		- [Class Table Inheritance](#class-table-inheritance)
		- [Concrete Table Inheritance](#concrete-table-inheritance)
		- [Inheritance Mappers](#inheritance-mappers)
	- [Object-Relational Metadata Mapping Patterns](#object-relational-metadata-mapping-patterns)
		- [Metadata Mapping](#metadata-mapping)
		- [Query Object](#query-object)
		- [Repository](#repository)

<!-- /TOC -->
- In PAEE, this is mainly concerned with relational databases, but can apply to other datasources like http req/resp, messaging etc
- Deals with data source layer
- Separates the mixing of db logic and application logic

## Good design

- Separate database code from other code (business and presentation)
  - provide database classes to access the db
  - all sql in same place
  - factories for each db
  - connection pools
  - Error handling
    - sql exceptions isolated to this layer
    - wrap as runtime exception

## Architectural patterns

- drive the way in which the domain logic talks to the database
- choice that's strongly affected by how you design your domain logic.
- choice you make here is far-reaching for your design and thus difficult to refactor
- Issues with database usage
  - Most people dont know how to write good sql, and should be tuned by experts (DBAs)

### Active Record

- Simple, for uncomplicated structures
- Each entity represents a table row and knows how to connect to the DB, persist itself to the DB and find other sibling objects from the DB, using static methods.
  - The entity has simple business logic
- Some domain logic might be in here or the calling code (ie transaction scripts)
- data structure (Fields) should match exactly the database table
- Good for
  - CRUD ops
  - Derivations and validations based on a single record
  - Work for single table
- Issues
  - it has an enormous amount of responsibilities, breaking the SRP
  - As complexity grows, and we refactor the domain objects into smaller objects, we lose the one-on-one mapping of objects to table rows and the pattern breaks.
  - logic and sql mixed, so hard to tests
  -  couples the object design to the database design. This
makes it more difficult to refactor either design

### Gateway

- The gateway represents a table in the DB and takes care of connecting, persisting and finding objects in the DB.
- simple as possible, generic, mechanic, reusable, maybe even generated. They should know nothing about business logic.
- make a direct mapping from table column to object property
- Usually stateless
- Types
  - Table Data Gateway
    - one instance  handles all rows in table.
    - used as mapping table to gateway
      - but you can have a single Table Data Gateway that handles all methods for all table
    - works well with Table Module.
    - Good place to have stored procedures
    - Can return appropriate domain object if accessed via domain layer
      - issue - you then have bidirectional dependencies the domain objects and the gateway
        - Fix - use a data mapper
    - issues
      - How it handles returning 1 or many data from find queries
        - use of data transfer object
  - Row Data Gateway
    - handles single row in table. For each row a new instance is created.
      - acts as an object that exactly mimics a single record
    - contains only data access logic, it does NOT contain any Domain Logic.
    - works well with Transaction Script.
      - not worth using with domain model, instead use active record
    - With Metadata Mapping, It can be used for creating automatically built database access code.
    - Use a separate class for queries, that returns a this gateway
- Issues
  -  If changes are done to either the model or the DB, those changes need to be reflected in its counterpart.
    - fix - avoid changes in lots of places, by making the row gateway match exactly the db structure

### Data Mapper

- The data mapper makes the translation between a set of data and one or several objects and from an object into one or several tables.
- It can, and should, use some kind of entity management system to cache the objects that were already extracted from the DB.
- the concrete task of connecting, finding and persisting a set of data in the DB should be left to a data gateway.
  - implement a data mapper as a decorator around a data gateway.
- Isolates the domain and data source layer, by having indirection layer, which maps the domain objects to the database tables
  - Allows both layers to vary independently
- Useful for more complex domain logic
  - So when trying to use patterns and oo, does not fit well with structure of database tables, this allows you to separate the domain and data layer, to allow domain to take advantage of patterns etc
  - This mean data needs to be transferred between between domain and data layer, which needs transformed to meet each layers needs
- whole layer of Data Mapper can be substituted, either for testing purposes or to allow a single domain layer to
work with different databases
-  Mappers need a variety of strategies to handle classes that turn into multiple fields, classes that have multiple tables, classes with inheritance, and the joys of connecting together objects once they've been sorted out.
- to inserts and updates, the database mapping layer needs to understand what objects have changed, which new ones have been created, and which ones have been destroyed. It also has to fit the whole workload into a transactional framework.
  - The Unit of Work

## Object-Relational Behavioural Patterns

- Repeatedly persisting and loading the same object to/from the DB can have a severe impact in performance
- need to prevent concurrently changing and persisting different instances that represent the same data
- Need to keep track of the objects that are loaded, in order to:
  - Not read an object from the DB more than once
  - Not write an object to the DB more than once
  - Always use the same object version for all editing operations (prevent concurrency)
  - Limit the entity nested graph loaded

### Unit of work

- Maintains a list of objects affected by a business transaction and coordinates the writing out of changes and the resolution of concurrency problems.
- keeps all this information in one place
  - encapsulated and dont have to worry about it
- platform for more complicated situations, such as handling business transactions that span several system transactions using locking
- Avoids making to many calls to the DB
  - Make changes to objects (in memory) and submit all changed objects in one or few calls
- let it know about objects you've read so that it can check for inconsistent reads by verifying that none of the objects changed on the database during the business transaction.
- Implementation
  - when it comes time to commit, the Unit of Work decides what to do. It opens a transaction, does any concurrency checking and writes changes out to the database
    - Good
      - Application programmers never explicitly call methods for database updates. This way they don't have to keep track of what's changed or
      - worry about how referential integrity affects the order in which they need to do things
  -  create a snapshot of the entity when loading it and comparing each managed entity to its snapshot when flushing the managed data into the DB, so that we only persist the modified objects.
    - Object is loaded is registered as clean, modified state changed to dirty, only write dirty state objects to DB
    - Good
      - allows for transparency (implicit persistence of changed entities)
      - decoupling of the entity from the UoW
    - Bad
      - adds some computation overhead
  - How to keep track of objects that have changed
    - the caller doing it (Called registration)
      - Any objects that aren't registered won't be written out on commi
      - Can lead to forgetfulness, but give flexibility to make changes that dont need to be committed
        - Better to have a copy do such thigns
    - by getting the object to tell the Unit of Work (object registration)
      - place registration methods in object methods. Loading an object from the database registers the object as clean
      - the Unit of Work needs either to be passed to the object or to be in a well-known place
      - the developer of the object has to remember to add a registration call in the right places.
      - Good place for ASP
    - Unit of work controller
      -  Unit of Work handles all reads from the database and registers clean objects whenever they're read. Rather than marking objects as dirty the Unit of Work takes a copy at read time and then compares the object at commit time
      - Good
        - it allows a selective update of only those fields that were actually changed
        -  avoids registration calls in the domain objects
- For testing
  -  providing a transient constructor that doesn't register with the Unit of Work
  - providing a Special Case Unit of Work that does nothing with a commit
- When
  - update order when a database uses referential integrity.
    - Most of the time you can avoid this issue by ensuring that the database only checks referential integrity when the transaction commits rather than with each SQL call
    - In smaller systems this can be done with explicit code that contains details about which tables to write first based on the foreign key dependencies.
    - In a larger application it's better to use metadata to figure out which order to write to the database.
  - minimize deadlocks
    - If every transaction uses the same sequence of tables to edit, you greatly reduce the risk of deadlocks.
    - to hold a fixed sequence of table writes so that you always touch the tables in the same order.
  - handling batch updates
    - a batch update is to send multiple SQL commands as a single unit so that they can be processed in a single remote call.
      - For DB chagnes are sent in rapid succession
    - Example impl
      - JDBC  -> to batch individual statements
      - manual -> building up a string that has multiple SQL statements and then submitting as one statement
- Alternative
  - to explicitly save any object whenever you alter it.
    - may get many more database calls than you want since
  - can leave all your updates to the end, by keeping  track of all the objects that have changed.
    - use variables in your code for this, but they soon become unmanageable once you have more than a few
  - give each object a dirty flag that you set when the object changes. Then you need to find all the dirty objects at the end of your transaction and write them out
    - Depends on how easy it is to find the dirty flags
    -  Domain model hierachy is hard to traverse compared to a single hierachy
  -
### Identity Map

- Ensures that each object gets loaded only once by keeping every loaded object in a map. Looks up objects using the map when referring to them
  - During the sessions (req/resp or message processing)
-  identity map is the structure that is used by the unit of work to keep track of the loaded entities.
  - Load once from database, read and update many in memory
-  a caching mechanism, but its primary goal is to maintain unique entities in memory.
- Improving consistency
  - ie updating the same row twice inconsistently
- Not for performance
- Good
  - Only load once from database
  - acts as a cache for database reads
  - Avoid update conflicts within a singlesessions
- Bad
  - Can store a lot of data
  - If there are changes in database, will be dealing with out of date data in map.
    - Deal with only inmemory data
    - Reload into map, when transaction is done or after time and inmem data has not be changed
  - If data is lost in map (ie app crashes), then database is not updated, thus db has stale data
    - Can use persistent cache
- when to use
  - If for immutable objects, may not need it
    - no need to worry about modification issues
    - but still useful as cache and  helps to prevent the use of the wrong form of equality test
  - Dont need for dependent mappings
    - as persistance controlled by parent
  - Not helpful for updates that cross sessions
- Implemetation
  -  have a series of maps containing objects that have been pulled from the database
  - an isomorphic schema, you'll have one map per database table.
  - When you load an object from the database, you first check the map. If there's an object in it that corresponds to the one you're loading, you return it.
    - If not, you go to the database, putting the objects into the map for future reference as you load them
  - Keys of map
    - primary key of the corresponding database table
      - This works well if the key is a single column and immutable.
    -  A surrogate primary key fits in very well with this approach because you can use it as the key in the map.
    - should be simple type, so comparisons are easy
    - encapsulating different kinds of database key behind a single key object.
  - Explicit or Generic
    -  explicit Identity Map is accessed with distinct methods for each kind of object you need
      - ie findPerson(1)
      - Good
        - Compile time checkign
        - explicit interface
          - it's easier to see what maps are available and what they're called.
          - Specific methods for each table/map, tailor made for application
      - Bad
        - Need to constantly update methods, and maps when new table exists
    - A generic map uses a single method for all kinds of objects, with perhaps a parameter to indicate which kind of object you need,
      - ie find("Person", 1).
      - Good
        - Can be resuable, and dont need to create new one every time a new table or map is created
      - Bad
        - Too abstract, specific methods might meet your needs
        - Runtime (ie reflection)
        -  only use a generic map if all your objects have the same type of key.
  - Amount
    - one map per class and one map for the whole session
    - A single map for the session works only if you have database-unique keys
      - Once you have one Identity Map, the benefit is that you have only one place to go and no awkward decisions about inheritance.
      - you don't have to add new ones when you add database tables.
    - one map per class/table
      - for multiple maps
       -   issues - need transactional protection
      - if your database schema and object models are the same
      - If different schemas, better have the maps based on the objects
    - Issues with inheritance
      - Keeping them separate can make polymorphic references much more awkward, since any lookup needs to know to look in all maps
      -  use a single map for each inheritance tree, but that means that you should also make your keys unique across inheritance trees
  - Location
    - Easy to find
    - Tied to the process context you are working in
    - ensure that each session gets it's own instance that's isolated from any other session's instance
      -  put the Identity Map on a session-specific object
      - Place in unit of work
      - Place in a registry thats tied to the session
    - Use of multiple maps means need of transactional protection
      - Can use object database as a transactional cache
    - Read only data
      - No need to worry about sharing across sessions
      - In performance-intensive systems it can be very beneficial to load in all read-only data once and have it available to the whole process
      - read-only Identity Maps held in a process context and your updatable Identity Maps in a session context
      - rarely updated
        - Can treat as read only
        - Can flushing the process-wide Identity Map and potentially bouncing the server when it happens

### Lazy Loading

- An object that doesn’t contain all the data you need but know how to get it.
  - Deals with rich data models and loading object hierarchies
- An object does not contain all of the data you need but knows how to get it
- When we have many nested entities, when loading one entity from the DB, we may end up loading a huge set of data that maybe we don’t even need.
- using lazy loading we store a reference to the nested entity, instead of the entity itself.
  - When we first access the nested entity we load the entity from the DB.
- Good
  - Save time and resources.
  - Avoids loading lots of data at the start, but only when needed
- Bad
  - Adds complexity, needs a good case to use
  -  “ripple loading”, aka “N+1 problem”,  which happens when we have a list of entities with nested lazy loaded entities. When we loop through the list, we will be loading the nested entities one by one, instead of all in one go.
    - Fix - use eager loading (pre-load the nested entities) when loading lists of entities.
  -  Lazy Load is that it can easily cause more database accesses than you need.
    - Fix -  is never to have a collection of Lazy Loads but, rather make the collection itself a Lazy Load and, when you load it, load all the contents.
      - limitation of this tactic is when the collection is very large
- How
  - lazy init
    - simple
    - every access to the field checks first to see if it's null. If so, it calculates the value of the field before returning the field
    - have to ensure that the field is self-encapsulated, meaning that all access to the field, even from within the class, is done through a getting method.
    - Using a null to signal a field that hasn't been loaded yet
      - unless null is a valid value, need a special case to use as check to start lazy loading
    - Bad
      - Dependency between object and database, works well with active record and table/row data gateway
  - Virtual Proxy
    - Used with data mapper
    - layer of indirection
    - object that looks like the object that should be in the field, but doesn't actually contain anything. Only when one of its methods is called does it load the correct object from the database.
    - Good is replacable for the object that should be there
    - Bad - it is not the same object, can have identity issues (ie for comparisons)
      - need to override equals
    - Bad - lots of proxies might be needed
    - can have more than one virtual proxy for the same real object. All of these proxies will have different object identities, yet they represent the same conceptual object.
    - https://www.educative.io/answers/what-is-the-virtual-proxy-design-pattern
  - value holder
    -  object that wraps some other object. To get the underlying object you ask the value holder for its value, but only on the first access does it pull the data from the database.
    - Bad -  the class needs to know that it's present and that you lose the explicitness of strong typing
      - fix - ensuring that the value holder is never passed out beyond its owning class.
  - ghost
    - is the real object in a partial state
    - When you load the object from the database it contains just its ID. Whenever you try to access a field it loads its full state
    - an object, where every field is lazy-initialized in one fell swoop, or as a virtual proxy, where the object is its own virtual proxy
    - instead of loading all data in one go, can load in groups instead
    - you can put it immediately in its Identity Map
      - avoid all problems due to cyclic references when reading in data
    - Inheritance often poses a problem with Lazy Load.
      - , you'll need to know what type of ghost to create, which you often can't tell without loading the thing properly
  - If data is quick to get hold of or commonly used, can fetch that first
  - Lazy Load is a good candidate for aspect-oriented programming. You can put Lazy Load behavior into a separate aspect, which allows you to change the lazy load strategy separately as well as freeing the domain developers from having to deal with lazy loading issue
  - have separate database interaction objects for the different use cases.
    - ie one with eager and one with lazy loads, and let code decide which to use (ie via strategy)
  - Have a range of degrees of laziness
    - you really need only two: a complete load and enough of a load for identification purposes in a list. Adding more usually adds more complexity than is worthwhile.
- When to use
  -  deciding how much you want to pull back from the database as you load an object, and how many database calls that will require
  - pointless to use Lazy Load on a field that's stored in the same row as the rest of the object, because most of the time it doesn't cost any more to bring back extra data in a call, even if the data field is quite large
  -  only worth considering Lazy Load if the field requires an extra database call to access.
  -  deciding when you want to take the hit of bringing back the data
    - good idea to bring everything you'll need in one call so you have it in place, particularly if it corresponds to a single interaction with a UI.
    - **The best time to use Lazy Load is when it involves an extra call and the data
you're calling isn't used when the main object is used.**

### Reading Data

- Its often better to pull out more rows and filter out the ones not needed then issuing one query for each row.

## Object-Relational Structural Patterns

### Identity Field
### Foreign Key Mapping
### Association Table Mapping
### Dependent Mapping
### Embedded Value
### Serialized LOB
### Single Table Inheritance
### Class Table Inheritance
### Concrete Table Inheritance
### Inheritance Mappers

## Object-Relational Metadata Mapping Patterns

### Metadata Mapping
### Query Object
### Repository
