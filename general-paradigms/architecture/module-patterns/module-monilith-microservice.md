# Module monolith vs Microservices

- Trend of always going for microservice rather than monolith, with out considering the implications 
- Better to think of mircoservices as the end goal, and start with modular monolith
- The main benefit of microservices that people promote is 
  - the idea of creating and maintaining small, independent "chunks" of code and data, versioned apart from one another, using common inputs and outputs to enable a larger integration of the system.
  - But modules allow the samething, with less of the issues of microsevices
- But the main benefit of microservices is 
  - organizational clarity
    - development team aggregating ownership of any and all of those dependencies that could (and frequently would) block them from moving forward.
    -  each team could build their artifact independently of one another
    - When the teams grow
    - Issues
      - hiring these folks became infinitely trickier, need to hire bigger skillset
  - Independently scalable
    - it's a critical factor
  - Independent releasability
  - Need to use diverse technologies to support business needs
    - Allows for greater flexibility
  - Manage complexity of the domain
  - Main issues 
    - https://architecturenotes.co/fallacies-of-distributed-systems/
      - When passing that data across network lines, though--as most microservices do--adds five to seven orders of magnitude greater latency to the communication
    - maintance - monitoring
    -  each service must be deployed independently, which increases the technical and operational complexity
    -  experience performance issues as a result of ‌increasing network traffic between services.
    - With increasing complexity, microservices might be more susceptible to mistakes and defects as well.
    - Hard to get right
    - lot of complexity
## Modular monolith
- A monolithic architecture is a singular, large computing network with one code base that couples all of the business concerns together. To make a change to this sort of application requires updating the entire stack by accessing the code base and building and deploying an updated version of the service-side interface.
- A Modular Monolith consists of dividing logic into modules, as each module is independent and isolated.
  - Every module is in charge of its own business logic, database or schema, etc. 
  - With this model of architecture, you can build and modify existing layers of each module while leaving the others unaffected.
  - Modules should communicate through APIs, allowing access to the logic of each module through public methods, not internal functions and the logic of each one.
- https://newsletter.techworld-with-milan.com/p/why-you-should-build-a-modular-monolith

## Benefits of modular monolity
- Modules circumvent a lot of the issues
  - when a system is decomposed into in-memory modules running on a single operating system node, the costs of passing data across process or library boundaries is pretty negligble
  - improve stability and perforamnce
- Faster to develop
- few moving parts, which makes it easier and quicker to accept modifications.
- Simpler to create, deploy and manage
  - the modules are produced and delivered as a single unit, which makes the application significantly easier to design, deploy and manage
- Cost effective

## disadvantage of monolith 
- how slow the development velocity is. Adding new features is slow because there is a large cognitive load on the developer. 
- Modules of monoliths are tightly coupled, which can significantly lengthen the release cycle of a monolith.
## Monolith to microservice 
- trying to turn a poorly structured monolith into a distributed architecture will only get you a... poorly structured, yet distributed architecture.
- Easier to go from modular monolith to microservice


## Links
- Modules or Microservices? - Sander Mak https://youtu.be/siHAu5sIIko
- https://blogs.newardassociates.com/blog/2023/you-want-modules-not-microservices.html
- https://www.cmsdrupal.com/blog/modular-monolith-vs-microservices-how-do-you-make-choice
