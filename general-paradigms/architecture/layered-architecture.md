# Layered Architecture

- Common style: UI/web -> Domain ->  Persistence
  - web depends on the domain, domain depends on the database(persistence layer)
- Can have more layers
- How it works
  - The web layer receives requests
  - routes them to a service/usecase in the domain or “business” layer
  - The service does some business magic
    - calls components from the persistence layer
      - to query for or
      - modify the current state of our domain entities.
- Allows for building domain, web and persistence as independent layers
  - Switch web or persistence layers with something else ie sql to nosql, http to files
  - Add Features without affecting other Features
- a good layered architecture we’re keeping our options open and are able to quickly adapt to changing requirements and external factors.

## Whats wrong with it

- Can allow bad habits to creep in, leave the app in a bad state  and hard to maintain or add features
- Need strong self discipline to avoid the following
  - but this discipline detrioates when deadlines occcur
- Promotes Database-Driven-Design
  - DB is the foundation of Layered Architecture
  - Any application aims is to model behaviour not state
    - behaviour changes state an drives business
  - Domain logic should be foundation of app
  - The app should start with the domain logic first, once correct then build persistence and web around it
  - ORM frameworks has led to intermixing of domain and persistence
    - using persistence objects in domain services will lead to coupling, especially if used via ORM
    - This fusion of domain and persistence leads rigid and hard to change app
- Prone to shortcuts
  - General rule in LA
    - the only global rule is that from a certain layer, we can only access components in the same layer or a layer below.
  - If we need access to a certain component in a layer above ours, we can just push the component down a layer and we’re allowed to access it.
    - bad
    - it couples higher levels with lower levels
    - The lower layers will grow fat, with more responsibilities
    - Global architectural rules should be enforced by devs and within the build
- It grows hard to test
  - Sometimes layers are skipped, ie web access the persistence directly
    - This scatters the domain logic, mixing responsibilities in different layers
  - Means having to mock domain and persistence layer in web layer, making tests complex
    - complex tests means less tests, as no one wants to do them or lack of time
  - This increase time, as it becomes harder to understand
- It hides the use cases
  - We change what exists more than adding new features
  - Finding where the domain logic is, is vital to get work done
  - architecture should help us navigate easily to the code to change or fix
  - Services become bloated, do lots of things/use cases,
    - This leads to many dependencies, hard  to tests
- It makes parallel work difficult
  - Teams can multiple devs working on the same code base at the same time
  - This can lead to merge conflicts, which takes up time
  - If each dev is working on different features, but the have to deal with the same code, it becomes slow
  - If we have a dev working in each layer, then should be able to have 3 devs working in parallel
    - Since everything builds on top of the persistence layer, the persistence layer must be developed first. Then comes the domain layer and finally the web layer. So only one developer can work on the feature at the same time
    -  but the developers can define interfaces first, you say, and then each developer can work against these interfaces without having to wait for the actual implementation
      - As long as no layers are coupled with each other ie database driven design
      - As long as we have narrow services which do one thing
  -

## Package structure

Example

```
1 App
2 ├──domain
3 |     ├── Account
4 |     ├── Activity
5 |     ├── AccountRepository (I)
6 |     └── AccountService
7 ├──persistence
8 |     └── AccountRepositoryImpl
9 └──web
10      └── AccountController
```

- Each layer has a package
  - This example has the DIP implemented
- Issues
  - we have no package boundary between functional slices or features of our application
    - Adding new features, can lead to a mess of classes in all layers/packages
  - we can’t see which use cases our application provides
    - What does AccountService do?? Not expressive
  - we can’t see our target architecture within the package structure
    - we can’t see at a glance which functionality is called by the web adapter and which functionality the persistence adapter provides for the domain layer. The incoming and outgoing ports are hidden in the code.
