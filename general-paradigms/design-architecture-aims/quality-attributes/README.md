# Qaulity Attributes

- AKA Non functional requirements
- It is a measurable or testable property of a system that is used to indicate how well the system satisfies the needs of its stakeholders.
  - as measuring the "goodness" of a product along some dimension of interest to a stakeholder.
- use quality attribute scenarios as a means of characterizing quality attributes and their requirements
  - should be unambiguous and testable.
  - Common form can include
    - Stimulus
      - describe an event arriving at the system
      - ie an event to the performance community, a user operation to the usability community, or an attack to the security community
    - Stimulus source
      -  may affect how it is treated by the system.
      - ie A request from a trusted user will not undergo the same scrutiny as a request by an untrusted user
    - Response.
      - consists of the responsibilities that the system (for runtime qualities) or the developers (for development-time qualities) should perform in response to the stimulus.
      - ie in a performance scenario, an event arrives (the stimulus) and the system should process that event and generate a response.
      - ie modifiability scenario, a request for a modification arrives (the stimulus) and the developers should implement the modification without side effects and then test and deploy the modification
    - Response measure
      - Determining whether a response is satisfactory
      - ie For performance this could be ameasure of latency or throughput
      - ie for modifiability it could be the labour or wall clock time required to make, test, and deploy the modification
    - Environment
      - the set of circumstances in which the scenario takes place
      - acts as a qualifier on the stimulus
      - ie request for a modification that arrives after the code has been frozen for a release may be treated differently than one that arrives before the freeze
      - A failure that is the fifth successive failure of a component may be treated differently than the first failure ofthat component.
    - Artifact
      - the portion ofthe system to which the requirement applies
      - ie whole system or component
- categories of quality attributes
  - those that describe some property of the system at runtime, such as availability, performance, or usability.
  - those that describe some property of the development ofthe system, such as modifiability or testability.
- quality attributes can never be achieved in isolation.
  - They are interlinked
  - there will be trade offs
  - Need to decide what takes precedence
  - Example
    - Take portability. The main technique for achieving portable software is to isolate system dependencies, which introduces overhead into the system's execution, typically as process or procedure boundaries, and this hurts performance.

## Requirements

- A system may several requirements it must perform
  - Functional requirements
  - Quality attribute requirements are qualifications of the functional requirements or of the overall product
    - A qualification of a functional requirement is an item such as how fast the function must be performed, or how resilient it must be to erroneous input
    - A qualification of the overall product is an item such as the time to deploy the product or a limitation on operational costs.
  - Deal with constraints
    - A constraint is a design decision with zero degrees of freedom
    - it's a design decision that's already been 1nade.
    - Examples
      - the requirement to use a certain programming language
      - to reuse a certain existing module
    - Choices are due to the architect in general
      - external factors might affect these
        - money
        - training
        - business agreements

## Design decisions

-  can view an architecture as the result of applying a collection of design decisions.
- categories might overlap, as long as known the concern ofthe architect is to ensure that every important decision is considered.

### Allocation of Responsibilities

- Include
  -  Identifying the important responsibilities, such as:
    -  basic system functions
    - architectural infrastructure
    - satisfaction of quality attributes
  - Determining how these responsibilities are allocated to non-runtime and runtime elements
    - such as modules, components, and connectors
- Strategies for making these decisions
  - functional decomposition
  - modeling real-world objects
  - grouping based on the major modes of system operation, or grouping based on similar quality requirements:
    - processing frame rate, security level, or expected changes

### Coordination Model

- Software works by having elements interact with each other through designed mechanisms
  - These mechanisms are collectively referred to as a coordination mode
- Decision:
  - Identifying the elements ofthe system that must coordinate, or are prohibited from coordinating
  - Determining the properties of the coordination, such as timeliness, currency, completeness, correctness, and consistency.
  - Choosing the communication mechanisms that realize those properties
    - mechanisms such as
      - between systems
      - between our system and external entities
      - between elements of our system
    - Properties include
      - stateful versus stateless
      - synchronous versus asynchronous
      -  guaranteed versus nonguaranteed delivery
      - performance-related properties such as throughput and latency

### Data Model

- Every system must represent artifacts of system-wide interest data in some internal fashion
- Decisions:
  - Choosing the major data abstractions, their operations, and their properties.
    - Includes
      - determining how the data items are created
      - initialized
      - accessed
      - persisted
      - manipulated
      - translated
      - destroyed
  - Compiling metadata needed for consistent interpretation of the data
  - Organizing the data.
    - Includes:
      - determining whether the data is going to be kept in a relational database, a collection of objects, or both.
        - If both, then the mapping between the two different locations of the data must be determined

### Management of Resources

- arbitrate the use of shared resources in the architecture
- Include:
  - hard resources
    - CPU
    - memory
    - battery
    - hardware buffers
    - system clock
    -  I/0 ports
  - soft resources
    - system locks
    - software buffers
    - thread pools
    - non-thread-safe code
- Desicions
  - Identifying the resources that must be managed and determining the limits for each
  - Determining which system element(s) manage each resource.
  - Determining how resources are shared and the arbitration strategies employed when there is contention.
  - Determining the impact of saturation on different resources
    - ie as a CPU becomes more heavily loaded, performance usually just degrades fairly steadily

### Mapping among Architectural Elements

- architecture must provide two types of mappings.
  - there is mapping between elements in different types of architecture structures
    - ie mapping from units of development (modules) to units of execution (threads or processes)
  - mapping between software elements and environment elements
    - mapping from processes to the specific CPUs or machines where these processes will execute
- Useful mappings
  - The mapping of modules and runtime elements to each other that is, the runtime elements that are created from each module; the modules that contain the code for each runtime element
  - The assignment of runtime elements to processors
  - The assignment of items in the data model to data stores
  - The mapping of modules and runtime elements to units of delivery

### Choice of Technology

- Every architecture decision must eventually be realized using a specific technology.
- decision can be made externally or by architect
- Choice of technology decisions
  - Deciding which technologies are available to realize the decisions made in the other categories.
  - Determining whether the available tools to support this technology choice (IDEs, simulators testing tools, etc.) are adequate for development to proceed
  - Determining the extent of internal familiarity as well as the degree of external support available for the technology (such as courses, tutorials, examples, and availability of contractors who can provide expertise in a crunch) and deciding whether this is adequate to proceed.
  - Determining the side effects of choosing a technology, such as a required coordination model or constrained resource management opportunities
  - Determining whether a new technology is compatible with the existing technology stack
    - can the new technology run on top of or alongside the existing technology stack?
    - Can it communicate with the existing technology stack?
    - Can the new technology be monitored and managed?


### Binding Time Decisions

-  introduce allowable ranges of variation
  - This variation can be bound at different times in the software life cycle by different entities from design time by a developer to runtime by an end user.
- A binding time decision establishes the scope, the point in the life cycle, and the mechanism for achieving the variation
- Examples
  - For allocation of responsibilities, you can have build-time selection ofmodules via a parameterized makefile
  - For choice of coordination model, you can design runtime negotiation of protocols
  - For resource management, you can design a system to accept new peripheral devices plugged in at runtime, after which the system recognizes them and downloads and installs the right drivers automatically
  - For choice oftechnology, you can build an app store for a smartphone that automatically downloads the version of the app appropriate for the phone ofthe customer buying the app.
- should consider the costs to implement the decision and the costs to make a modification after you have implemented the decision
  - Making this decision depends on the costs incurred by having to modify an early binding compared to the costs incurred by implementing the mechanisms involved in the late binding.
