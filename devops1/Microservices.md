# microservice

- A microservice architecture is the natural consequence of applying the single responsibility principle at the architectural level.
- Each microservice may or may not provide some form of user interface.
- This results in a number of benefits over a traditional monolithic architecture such as
  -  independent deployability
  - language
    - less coupling to a language or stack
  - platform and technology independence for different components
  - distinct axes of scalability
    - vertical scaling of parts of system rathe than whole monolith
  - increased architectural flexibility.
- size
  - Commonly, microservices are of the order of hundreds of lines but can be tens or thousands depending on the responsibility they encapsulate. A good, albeit non-specific, rule of thumb is as small as possible but as big as necessary to represent the domain concept they own.
  - https://bovon.org/archives/350
- integration
  - Microservices are often integrated using REST over HTTP. In this way, business domain concepts are modelled as resources with one or more of these managed by each service. In the most mature RESTful systems, resources are linked using hypermedia controls such that the location of each resource is opaque to consumers of the services
  - Alternative integration mechanisms are sometimes used such as
    - lightweight messaging protocols
    - publish-subscribe models
    - alternative transports such as Protobuf or Thrift.
- Often, microservices display similar internal structure consisting of some or all of the displayed layers/modules, within a network boundary
  - protocol
    - Resources
      - Resources act as mappers between the application protocol exposed by the service and messages to objects representing the domain.
      - Typically, they are thin, with responsibility for sanity checking the request and providing a protocol specific response according to the outcome of the business transaction.
      - ie webserver
  - Domain
    - Almost all of the service logic resides in a domain model representing the business domain.
    - Of these objects, services coordinate across multiple domain activities, whilst repositories act on collections of domain entities and are often persistence backed.
    - including
      - service layer
      - domain
      - respositories
  - External
    - If one service has another service as a collaborator, some logic is needed to communicate with the external service.
    - A gateway encapsulates message passing with a remote service, marshalling requests and responses from and to domain objects.
    - It will likely use a client that understands the underlying protocol to handle the request-response cycle.
    - including
      - Gateways
      - Clients
  - Persistenance
    - Except in the most trivial cases or when a service acts as an aggregator across resources owned by other services, a micro-service will need to be able to persist objects from the domain between requests.
    - Usually this is achieved using object relation mapping or more lightweight data mappers depending on the complexity of the persistence requirements.
    - Often, this logic is encapsulated in a set of dedicated objects utilised by repositories from the domain.
    - including
      - datamappers/orm
- Multiple microservices provide business features
  - Typically, a team will act as guardians to one or more microservices.
  - These services exchange messages in order to process larger business requests.
  - In terms of interchange format, JSON is currently most popular although there are a number of alternatives with XML being the most common.
  - In some cases, an asynchronous publish-subscribe communication mechanism suits the use case better than a synchronous point-to-point mechanism.
  - The Atom syndication format is becoming increasingly popular as a lightweight means of implementing pub-sub between microservices.
  - n larger systems, there are often multiple teams each with responsibility for different bounded contexts.
- In a microservice environment, we never understand the whole picture because it’s too complex.
- So why not go back to monoliths?
  - Because we want to be able to make cheap experiments.
  -  We want to quickly implement a certain feature and test it in production.
  - We want to release many times a day.
- To operate microservices successfully, DevOps is key. Only the developers really know what’s going on and can fix things.

## Advantages


## Why No need for Microservices

- https://medium.com/swlh/stop-you-dont-need-microservices-dc732d70b3e0
- https://completedeveloperpodcast.com/episode-189/


## links

- https://www.javacodegeeks.com/2018/03/introduction-to-microservices.html
- https://microservices.io/
- https://www.marcobehler.com/guides/java-microservices-a-practical-guide
- https://youtu.be/z8qhToMtYRc Microservices • Martin Fowler • YOW! 2016
