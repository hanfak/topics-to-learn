# Evolutionary Architecture

- answers 
  - How is long-term planning possible when everything changes all the time?
  
## Issues with current systems

- parts of software systems resist change, becoming more brittle and intractable over time
  - But requirements change, technology changes or needs updating, change is constant
  - For systems, and by extension businesses based on them, to stay working or used they need to change as well
- Change is a constant, but we can never fully predicate what is likely to change
  - ie unknown changes in requirements, breaking changes in libraries, security vulnerabilities exposed

## What 

- An evolutionary architecture supports guided, incremental change across multiple dimensions
- allow architects and developers to make sweeping changes to the most important parts of their systems with confidence.
- evolve cleanly without the need for a crystal ball.

### Incremental Change 

- To achieve this can use a variety processes and tools 
  - continuous delivery practices like deployment pipelines
  - mature DevOps
  - good testing culture
  - other current agile engineering best practices
  - granular, modular architecture
- For  “how teams build software” and “how they deploy it.”
- in a service architecture, ensure that clients can upgrade at their own pace rather than assuming all clients will upgrade immediately and synchronously as they won’t.
- automate the deprovisioning of unused services and versions once they stop receiving traffic
- versioning services internally instead of clients passing versions
  - This fingerprints incoming requests and routes them to the correct implementation, but the endpoint that clients call doesn’t change
  - limit the number of supported versions
  - strive to support only two versions at a time, and only temporarily
- Testability is essential
  - supporting a rapid development loop
- Follow hypothesis-driven development
  - rather than gathering formal requirements… leverage the scientific method instead

### Fitness Functions 

- An architectural fitness function provides an objective integrity assessment of some architectural characteristic(s).
- Guide change
- preferably as unit tests that can be run locally
- we don’t want the system to evolve in a way that harms some architectural concern
- build guidelines within the architecture to support change but guard specific attributes
- an objectively quantifiable function used to summarise how close a given design solution is to achieving the set aims
- defines what “better” means 
- are run in your deployment pipeline, removing the architect from the gatekeeper role, and instead allowing them to focus on guiding rather than enforcing.
- Should be designed as early in a project’s lifecycle as possible, because they serve as a ratchet on quality degradation
- These should be adpated, or new ones added on a periodic basis as you know more about the system
  - meet often to re-evaluate
  - use them to have a structured conversation as early as possible
  
#### Types
  - Atomic 
    - run against a singular context and exercise one particular aspect of the architecture
    - ie asserting there are no incompatible dependencies for a codebase.
  - Holistic
    - run against a shared context and exercise a combination of architectural aspects such as security and scalability
    - ie Ensuring that no personally identifying information (PII) is published into your logging system
    - ie Monitoring that latency doesn’t increase with code changes
    - Triggered
      - run based on a particular event, such as a developer executing a unit test
      - verifications run on demand in your deployment pipeline, during local development and so on: 
        - linting, tests, fuzzing, coverage
    - Continual
      - don’t run on a schedule, but instead execute constant verification
      - ie alerts on latency or ensuring infrastructure costs are trending towards budget
    - Static
      - have a fixed result, such as the binary pass/fail of a unit test.
      - ie acceptable latency range, acceptable test coverage, unit tests passing
    - Dynamic 
      - rely on a shifting definition based on extra context
      - ie embody a tradeoff between say freshness and request volume, tolerating less freshness (and consequently more caching) for high volume infrastructure
    - Automated 
    - Manual 
    
## Multiple dimensions

- Instead of focusing on just the technical aspects
  - ie  the technical architecture: frameworks, dependencies, integration architecture
- Should focus on other orthogonal concerns: data architecture, security, scalability, testability, operations etc
- All required dimensions, deemed critical, should be accommodated continuously

## Architectural coupling

- Modularity 
  - a logical grouping of related code
  - one of the most important tools to limit architectural coupling
  - Create modules out of related functionality to maximize functional cohesion
  - Aiming to scope modules as architectural quantum, 
    - an independently deployable component with high functional cohesion
- Small modules are easier to change, so generally prefer smaller, 
  - but getting the right boundaries is key to balance between coupling and complexity
- The style of codebases (ie monolith, mircoservice etc) is less importnat (as long as it meets your needs) than desingning the implementation well

## Evolutionary data

- heaviest frictions for evolving architecture is the underlying data
- Includes data as 
  - test
  - versioned
  - incremental
- have shared-nothing architecture 
  - where applications don’t directly integrate against the same database
  - IF sharing db
    - consider the “expand/contract pattern”, which allows you to support broader functionality, transition incrementally, and then remove the old using a combination of code rewriting, code ratchets
- inappropriate data coupling
  - for example transactions force large architectural quanta
  - Anything within a transaction needs to be deployed with the other pieces contributing to that transaction
  - Transactions are also often owned by a database administration or infrastructure team, which introduce cross-team coordination aspects as well.
- how weak DBA tooling is
  - compared to IDE
  - due to vendor lock in

## How 

- Remove needless variability
  - through adoption of immutable infrastructure, long-lived feature flags
- Make decisions reversible
  - making it easy to undo deploys
  - Prefer immediately shifting traffic off a broken new version to slowly deploying a previous revision
  - Prefer flipping flags to disable new features over deployment
- Prefer evolvable over predictable
  - If you optimize for the known challenges for an architecture, you’ll get stuck because there are at least as many unknown challenges as known challenges
  - better to be able to respond to problems quickly than to cleanly address what you’re currently aware of
- Build anticorruption layers
  - building good interfaces so you can shift out the implementation underneath
  - act of adding interfaces can be expensive as well, so balance this with finding the last responsible moment to make the decision.
- Build sacrificial architectures
  - Assume that you’ll make tradeoffs that won’t last forever, and be okay with occasionally throwing away your implementations
- Mitigate external change
  - don’t rely on global package repositories, but instead pull in copies of packages you need locally. Then you can manage your upgrade timing in addition to owning your build pipeline reliability
- Libraries versus frameworks
  - Argues against frameworks, since you write code that integrates with frameworks, as opposed to writing code that calls out to libraries. 
  - Consequently, there is tighter coupling in frameworks
- Version services internally
  - don’t leak version identifiers to users, instead inspect the incoming requests and handle them appropriately
  - Easier for service to manage that complexity than all clients to handle it
- Product over project
  - Structure your teams, and consequently your architecture, around long-lived products, not to short-lived projects
- Dealing with external change
  - Your clients (as in, software generating requests to your service) will change their needs over time, 
  - define explicit contracts to state these agreements, perhaps as Service Level Objectives.
- Culture of experimentation
  - Evolution is built on structured, measured experimentation, which requires a structured, thoughtful approach
- Start with low-hanging fruit
  - Easy wins beget larger wins, start where it’s easy
  -  start first where most changes happen 

## Links 
- https://lethain.com/building-evolutionary-architectures/
- 