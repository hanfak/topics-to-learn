# Availability

- It is a property of software that **it is there and ready to carry out its task when you need it to be.**
  - Includes reliability and downtime for maintaince
  - Builds on reliability, by adding recoverability
    - **Recoverability - when the system breaks, it repairs itself**
  - availability is about **minimizing service outage time by mitigating faults.**
- AKA Dependability is the ability to avoid failures that are more frequent and more severe than is acceptable
  - Fault tolerant
- **Availability refers to the ability of a system to mask or repair faults/failures such that the cumulative service outage period does not exceed a required value over a specified time interval.**
  - Failures, which affect the availability, is subject to the judgment of an external agent, possibly a human
    - Hence other quality attributes such as reliability, confidentiality, integrity and and anything else that causes unacceptable failures
    - Failure implies visibility to a system or human observer in the environment
    - **a failure is the deviation of the system from its specification, where the deviation is externally visible**
      - A failure occurs when the system no longer delivers a service that is consistent with its specification; this failure is observable by the system's actor
    - **A Fault (or combination of faults) is the cause of the failure **
      - A fault can be either internal or external to the system
      - **Errors - Intermediate states between the occurrence of a fault and the occurrence of a failure**
      - Faults can be prevented, tolerated, removed, or forecast
      - faults are detected and correlated prior to being reported and repaired
      - Fault correlation logic will categorize a fault according to its severity (critical, major, or minor) and service impact (service-affecting or non-service-affecting) in order to provide the system operator with timely and accurate system status and allow for the appropriate repair strategy to be employed.
      - The repair strategy may be automated or may require manual intervention.
- Availability is closely related to security
  - DDoS/DoS attacks designed to make a system fail that is, to make it unavailable
- Availability is also closely related to performance
  - it may be difficult to tell when a system has failed and when it is simply being outrageously slow to respond
  - A slow system is just as bad and seen as the same as donw service
-  availability is closely allied with safety
  - **Safety - keeping the system from entering a hazardous state and recovering or limiting the damage when it does**
- Building HA systems, need to understand the nature of the failures that
can arise during operation and provide mitgation strategies for them
  - We care about:
    - how system faults are detected
    - how frequently system faults may occur
    - what happens when a fault occurs
    - how long a system is allowed to be out of operation, when faults or failures may occur safely
    - how faults or failures can be prevented
    -  what kinds of notifications are required when a failure occurs
    - the level of capability that remains when a failure has occurred
  - Because a system failure is observable by users, the time to repair is the time until the failure is no longer observable
  - observability (making a system processes/state observable) is another quality attribute linked to availability
- automatic repair strategies
  - if code containing a fault is executed but the system is able to recover from the fault without any deviation from specified behavior being observable, there is no failure
- availability of a system  = MTBF / ( MTBF + MTTR)
  - MTBF = the mean time between failures
  - MTTR = the mean time to repair
  - As a percentage
    - like 5 9's = 99.999% available, thus only 0.001% downtime
      - downtime = 1m18s per 90 days, 5m15s per year
    - Although scheduled downtime (repairs) are sometimes not conisdered part of this calculation
    - This % is used in SLAs (service-level agreement)
      - specifies the availability level that is guaranteed and, usually, the penalties that the computer system or hosting service will suffer if the SLA is violated
  - helps you think about
    - what will make your system fail
    - how likely that is to occur
    - that there will be some time required to repair it

## Planning for failure

- planning for failure is not an option, is impossible and inevitable
- Better to plan for the occurrence of failure or (more likely) failures, and handling them
- Need to understand the possible failures and what their consequences are
  - Methods:
    - Hazard Analysis
      -  attempts to catalog the hazards that can occur during the operation of a system
      - categorizes each hazard according to its severity
      - Different fields have set standards of categories
      - assesses the probability of each hazard occurring
      - Hazards for which the product of cost and probability exceed some threshold are then made the subject of mitigation activities.
    - Fault tree analysis
      - an analytical technique that specifies a state ofthe system that negatively impacts safety or reliability, and then analyzes the system's context and operation to find all the ways that the undesired state could occur
      - uses a graphic construct (the fault tree) that helps identify all sequential and parallel sequences of contributing faults that will result in the occurrence of the undesired state, which is listed at the top ofthe tree (the "top event")
      - Can find  a "minimal cut set" is the smallest combination of events along the bottom of the tree that together can cause the top event.
        - The set ofminimal cut sets shows all the ways the bottom events can combine to cause the overarching failure.
        - Any singleton minimal cut set reveals a single point of failure, which should be carefully scrutinized.
      - the probabilities of various contributing failures can be combined to come up with a probability ofthe top event occurring
      - Dynamic analysis occurs when the order of contributing failures matters
        -  Markov analysis can be used to calculate probability of failure over different failure sequences
      - used to diagnose failures at runtime
        - If the top event has occurred, then (assuming the fault tree model is complete) one or more ofthe contributing failures has occurred, and the fault tree can be used to track it down and initiate repairs
    - Failure Mode, Effects, and Criticality Analysis (FMECA)
      - catalogs the kinds of failures that syste1ns of a given type are prone to, along with how severe the effects of each one can be
      - relies on the history of failure of similar systems in the past
  - These methods are only as good as the knowledge and experience of the people who populate their respective data structures.
    - don't let safety engineering become a matter ofjust filling out the tables.
    - keep pressing to find out what else can go wrong, and then plan for it

## General Scenario

- Source of stimulus
  - We differentiate between internal and external origins of faults or failure because the desired system response may be different
  - ie
    - people
    - hardware
    - software
    - physical infrastructure
    - physical environment
- Stimulus
  - A fault of one ofthe following classes occurs:
    - Omission = A component fails to respond to an input
    - Crash = The component repeatedly suffers omission faults
    - (Incorrect) Timing = A component responds but the response is early or late
    - (Incorrect) Response = A component responds with an incorrect value
-  Artifact
  -  specifies the resource that is required to be highly available, such as:
    - processor
    - communication channel
    - process
    - storage
- Environment
  - The state of the system when the fault or failure occurs may also affect the desired system response.
    - Normal operation
    - startup
    - shutdown
    - repair mode
    - degraded operation
    - over1oaded operation
  - For example, if the system has already seen some faults and is operating in other than normal mode, it may be desirable to shut it down totally. However, if this is the first fault observed, some degradation of response time or function may be preferred
- Response
  - There are a number of possible reactions to a system fault
  - First, the fault must be detected and isolated (correlated) before any other response is possible
    - One exception to this is when the fault is prevented before it occurs.
    - Actions associated with these possibilities include
      - logging the failure
      - notifying selected users or other systems
  - After the fault is detected, the system must recover from it
    - Actions associated with these possibilities include
      - taking actions to limit the damage caused by the fault
      - Disable source of events causing the fault
      - switching to a degraded mode with either less capacity or less function
      - shutting down external systems
      - becoming temp unavailable during repair
      - Fix or mask the fault/failure or contain the damage it causes
- Response measure
  - The response measure can specify
    -  an availability percentage
    - it can specify
      - a time to detect the fault
      - time to repair the fault
      - times or time intervals during which the system must be available
      - the duration for which the system must be available.

## Tactics

- Availability tactics are designed to enable a system to endure system faults so that a service being delivered by the system remains compliant with its specification
- aim
  -  keep faults from becoming failures
  - at least bound the effects of the fault and make repair possible.
- often the case that these tactics will be provided for you by a software infrastructure, such as a middleware package
- **Detect Faults**
  - the presence of the fault must be detected or anticipated before taking action on the fault
  - Tactic: Ping/echo
    - an asynchronous request/response message pair exchanged between nodes, used to determine reachability and the round-trip delay through the associated network path.
    - the echo also determines that the pinged component is alive and responding correctly
    - ping is often sent by a system monitor
    - requires a time threshold to be set; this threshold tells the pinging component how long to wait for the echo before considering the pinged component to have failed ("timed out").
    - There are standard implementations for this ie for ip
  - Tactic: Monitor
    - is a component that is used to monitor the state ofhealth ofvarious other parts ofthe system: processors, processes, 1/0, memory, and so on
      - monitor key components of a system and detect malfunctions
        - ie third party services, database connections
        - incomplete processes, processes in failed state
    - A system monitor can detect failure or congestion in the network or other shared resources
  - Tactic: Heartbeat
    -  a fault detection mechanism that employs a periodic message exchange between a system monitor and a process being monitored
    - For systems where scalability is a concern, transport and processing overhead can be reduced by piggybacking heartbeat messages on to other control messages being exchanged between the process being monitored and the distributed system controller.
    -  The big difference between heartbeat and ping/echo is who holds the responsibility for initiating the health check the monitor or the component itself
  - Tactic: Time stamp
    - used to detect incorrect sequences of events, primarily in distributed message-passing systems
    - A time stamp of an event can be established by assigning the state of a local clock to the event immediately after the event occurs.
    - Simple sequence numbers can also be used for this purpose, iftime information is not important.
  - Tactic: Sanity checking
    - checks the validity or reasonableness of specific operations or outputs of a component.
    - based on
      - a knowledge ofthe internal design
      - the state of the system
      - the nature of the information under scrutiny
    - most often employed at interfaces, to examine a specific information flow
  - Tactic:Condition monitoring
    - checking conditions in a process or device, or validating assumptions made during the design
    - prevents a system from producing faulty behavior
    - ie  computation of checksum
    - the monitor must itself be simple (and, ideally, provable) to ensure that it does not introduce new software errors.
  - Tactic: voting
    - implemented triple modular redundancy (TMR)
      - which employs three components that do the same thing, each of which receives identical inputs, and forwards their output to voting logic, used to detect any inconsistency among the three output states
    - Faced with an inconsistency, the voter reports a fault.
    - It can let the majority rule, or choose some computed average of the disparate outputs
    - voting schema is important
      -  which is usually realized as a simple, rigorously reviewed and tested singleton so that the probability of error is low
    - Types of voting
      - Replication
        - is the simplest form ofvoting;
        - the components are exact clones of each other.
        - Having multiple copies of identical components can be effective in protecting against random failures of hardware
          - but this cannot protect against design or implementation errors, in hardware or software, because there is no form of diversity embedded in this tactic
      - Functional redundancy
        - is a form of voting intended to address the issue of common-mode failures (design or implementation faults) in hardware or software components.
        - the components must always give the same output given the same input, but they are diversely designed and diversely implemented.
      - Analytic redundancy
        - permits not only diversity among components' private sides, but also diversity among the components' inputs and outputs
        - intended to tolerate specification errors by using separate requirement specifications
        - The voter mechanism used needs to be more sophisticated than just letting majority rule or computing a simple average
        - it may have to understand which sensors are currently reliable or not, and it may be asked to produce a higher-fidelity value than any individual component can, by blending and smoothing individual values over time
  - Tactic: Exception detection
    - the detection of a system condition that alters the normal flow of execution
    - Tactic: System exceptions
      - will vary according to the processor hardware architecture employed and include faults such as divide by zero, bus and address faults, illegal program instructions, and so forth.
    - Tactic: parameter fence
      - incorporates an a priori data pattern (such as OxDEADBEEF) placed immediately after any variable-length parameters of an object
      - allows for runtime detection of overwriting the memory allocated for the object's variable-length parameters.
    - Tactic: Parameter typing
      - employs a base class that defines functions that add, find, and iterate over type-length-value (TLV) formatted message parameters
      - Derived classes use the base class functions to implement functions that provide parameter typing according to each parameter's structure.
      - Use of strong typing to build and parse messages results in higher availability than implementations that simply treat messages as byte buckets
      - When you employ strong typing, you typically trade higher availability against ease of evolution.
    - Tactic: Timeout
      - that raises an exception when a component detects that it or another component has failed to meet its timing constraints
      - ie a component awaiting a response from another component can raise an exception if the wait time exceeds a certain value
  - Tactic: Self-test
    - Components (or whole subsystems) can run procedures to test themselves for correct operation.
    - Self-test procedures can be initiated by the component itself, or invoked from time to time by a system monitor.
    - These may involve employing some of the techniques found in condition monitoring, such as checksums
- **Recover From faults**
  - Preparation-and-repair tactics
    - based on a variety of combinations of retrying a computation or introducing redundancy
    - Tactic: Active redundancy (hot spare)
      - a configuration where all of the nodes (active or redundant spare) in a protection group. receive and process identical inputs in parallel, allowing the redundant spare(s) to maintain synchronous state with the active node(s).
        - A protection group is a group ofprocessing nodes where one or more nodes are "active," with the remaining nodes in the protection group serving as redundant spares.
      - the redundant spare possesses an identical state to the active processor, it can take over from a failed component in a matter of milliseconds
      - aka "one plus one" redundancy
    - Tactic: Passive redundancy (warm spare)
      - to a configuration where only the active members of the protection group process input traffic
      - one of their duties is to provide the redundant spare(s) with periodic state updates
      - the state maintained by the redundant spares is only loosely coupled with that of the active node(s) in the protection group (with the looseness of the coupling being a function ofthe check pointing mechanism employed between active and redundant nodes)
        - the redundant nodes are referred to as warm spares
      - passive redundancy provides a solution that achieves a balance between the more highly available but more compute-intensive (and expensive) active redundancy tactic and the less available but significantly less complex cold spare tactic (which is also significantly cheaper)
    - Tactic: Spare (cold spare)
      - Cold sparing refers to a configuration where the redundant spares of a protection group remain out of service until a fail-over occurs, at which point a power-on-reset procedure is initiated on the redundant spare prior to its being placed in service.
      - Due to its poor recovery performance, cold sparing is better suited for systems having only high-reliability (MTBF) requirements as opposed to those also having high-availability requirements.
    - Tactic: Exception handling
      - Once an exception has been detected, the system must handle it in some fashion
      - The easiest thing it can do is simply to crash, but that's a terrible idea from the point of availability
      - Solutions
        - simple function return codes (error codes)
        - use of exception classes that contain information helpful in fault correlation
          - such as the name ofthe exception thrown, the origin of the exception, and the cause of the exception thrown
          - logging
      - Software/people can then use this information to mask the fault, usually by correcting the cause of the exception and retrying the operation
    - Tactic: Rollback
      - permits the system to revert to a previous known good state (rollback line) upon the detection of a failure
      - Once the good state is reached, then execution can continue.
        - or retry
      - combined with active or passive redundancy tactics so that after a rollback has occurred, a standby version ofthe failed component is promoted to active status
      - depends on a copy of a previous good state (a checkpoint) being available to the components that are rolling back
        - Checkpoints can be stored in a fixed location and updated
          - at regular intervals,
          - at convenient or significant times in the processing
            - such as at the completion of a complex operation
    - Tactic: Software upgrade
      - to achieve in-service upgrades to executable code images in a non-service-affecting manner
      - realized as
        - a function patch
          - used in procedural programming and employs an incremental linker/loader to store an updated software function into a pre-allocated segment of target memory
          - The new version of the software function will employ the entry and exit points of the deprecated function.
          - upon loading the new software function, the symbol table must be updated and the instruction cache invalidated.
          - deliver bug fixes
        - a class patch
          - for targets executing object-oriented code, where the class definitions include a back-door mechanism that enables the runtime addition of member data and functions.
          - deliver bug fixes
        - a hitless in-service software upgrade (ISSU)
          - leverages the active redundancy or passive redundancy tactics to achieve non-service-affecting upgrades to software and associated schema
          - deliver new features and capabilities
    - Tactic: retry
      - assumes that the fault that caused a failure is transient and retrying the operation may lead to success.
      - used in places where failures are common and expected
      - There should be a limit on the number of retries that are attempted before a permanent failure is declared
    - Tactic: Ignore faulty behavior
      -  ignoring messages sent from a particular source when we determine that those messages are spurious
      - ie  we would like to ignore the messages of an exten1al component launching a denial-of-service attack by establishing Access Control List filters
    - Tactic: degradation
      - maintains the most critical system functions in the presence of component failures, dropping less critical functions
      - done in circumstances where individual component failures gracefully reduce system functionality rather than causing a complete system failure.
    - Tactic: Reconfiguration
      - attempts to recover from component failures by reassigning responsibilities to the (potentially restricted) resources left functioning, while maintaining as much functionality as possible
      - load balancing
  - Reintroduction tactics
    - concerned with reintroducing a failed (but rehabilitated) component back into normal operation.
    - Tactic: shadow tactic
      - to operating a previously failed or in-service upgraded component in a "shadow mode" for a predefmed duration oftime prior to reverting the component back to an active role
      - During this duration its behavior can be monitored for correctness and it can repopulate its state incrementally
    - Tactic: State resynchronization
      - When used alongside the active redundancy tactic,
        - the state resynchronization occurs organically, because the active and standby components each receive and process identical inputs in parallel
        - the states of the active and standby components are periodically compared to ensure synchronization
        - Comparison based on
          - a cyclic redundancy check calculation (checksum)
          - for systems providing safety critical services, a message digest calculation (a one-way hash function)
      - When used alongside the passive redundancy (warm spare) tactic
        - state resynchronization is based solely on periodic state information transmitted from the active component(s) to the standby component(s), typically via checkpointing
      - A special case of this tactic is found in stateless services, whereby any resource can handle a request from another (failed) resource.
        - ie for services which are replicas
        - Issues with shared state ie in datastore
    - Tactic: Escalating restart
      - that allows the system to recover from faults by varying the granularity ofthe component(s) restarted and minimizing the level of service affected
      - useful for  graceful degradation,
        - where a system is able to degrade the services it provides while maintaining support for mission-critical or safety-critical applications.
    - Tactic: Non-stopforwarding (NSF)
      -  is a concept that originated in router design.
        - In this design functionality is split into two parts:
          - supervisory, or control plane (which manages connectivity and routing information)
          -  data plane (which does the actual work of routing
          - packets from sender to receiver).
        - If a router experiences the failure of an active supervisor, it can continue forwarding packets along known routes with neighboring routers while the routing protocol information is recovered and validated.
        - When the control plane is restarted, it implements what is sometimes called "graceful restart," incrementally rebuilding its routing protocol database even as the data plane continues to operate
  - **Prevent faults**
    - deal with runtime means to prevent faults from occurring
    - Best way to do this is before the system is running, by having high quality code
      - code reviews, pair programming, solid requirements reviews, testing coverage
    - Tactic: Removalfrom service/software rejuvenation
      - temporarily placing a system component in an outof-service state for the purpose ofmitigating potential system failures
      - ie taking a component of a system out of service and resetting the component in order to scrub latent faults (such as memory leaks, fragmentation, or soft errors in an unprotected cache) before the accumulation of faults affects service (resulting in system failure)
    - Tactic: Transaction
      - ensure that asynchronous messages exchanged between distributed components are atomic, consistent, isolated, and durable.
      - "two-phase commit protocol
        - prevents race conditions caused by two processes attempting to update the same data item.
    - Tactic: Predictive model
      -  monitor the state of health of a system process to ensure that the system is operating within its nominal operating parameters, and to take corrective action when conditions are detected that are predictive of likely future faults
    - Tactic: Exception prevention
      -  the purpose ofpreventing system exceptions from occurring.
    - Tactic: Increase competence set
      - A program's competence set is the set of states in which it is "competent" to operate
      - When a component raises an exception, it is signaling that it has discovered itself to be outside its competence set;
        - it doesn't know what to do and is throwing in the towel
      - Increasing a component's competence set means designing it to handle more cases faults as part of its normal operation

## Checklist for Availability

- Allocation of Responsibilities
  - Determine the system responsibilities that need to be highly available.
  - Within those responsibilit1es, ensure that additional responsibilities have been allocated to detect an
    - omission
    - crash
    - incorrect timing
    - incorrect response.
  - ensure that there are responsibilities to do the following:
    - Log the fault
    - Notify appropriate entities (people or systems)
    - Disable the source of events causing the fault
    - Be temporarily unavailable
    - Fix or mask the fault/failure
    - Operate in a degraded mode
- Coordination Model
  - Determine the system responsibilities that need to be 'highly available.
  - With respect to those responsibilities, do the following:
    - Ensure that coordination mechanisms can detect an omission, crash, incorrect timing, or incorrect response.
      - Consider, for example, whether guaranteed delivery is necessary.
      - Will the coordination work under conditions of degraded communication?
    - Ensure, that coordination mechanisms enable
      - the logging of the fault
      - notification of appropriate entities
      - disabling of the source of the events causing the fault
      - fixing or masking the fault
      - operating in a degraded mode.
    - Ensure that the coordination model supports the replacement of the artifacts used (processors, communications channels, persistent storage, and processes).
      - For example, does replacement of a server allow the system to continue to operate?
    - Determine if the coordination will work under conditions of
        -  degraded communication
        - at startup/shutdown
        - in repair mode
        -  under overloaded operation.
      - For example, how much lost information can the coordination model withstand and with what consequences?
- Data Model
  - Determine which portions of the system need to be highly avai1able.
    - Within those portions, determine which data abstractions, along with their operations or their properties, could cause
      - a fault of omission
      - a crash
      - incorrect timing behavior
      -  an incorrect response
  - For those data abstractions, operations, and properties, ensure that they can
    - be disabled
      - be temporarily unavailable
      - be fixed or masked in the event of a fault
  - For example, ensure that write requests are cached if a server is temporarily unavailable and performed when the server is returned to service.
- Mapping among Architectural Elements
  - Determine which artifacts (processors, communication channels, persistent storage, or processes) may produce a fault omission, crash, incorrect timing, or incorrect response.
  - Ensure that the mapping (or remapping) of architectural elements is flexible enough to permit the recovery from the fault.
    - This may involve a consideration of the following:
      - Which processes on failed processors need to be reassigned at runtime
      - Which processors. data stores, or communication channels can be activated or reassigned at runtime
      - How data on failed processors or storage can be served by replacement units
      - How quickly the system can be reinstalled based on the units of delivery provided
      - How to (re)assign runume elements to processors, communication channels, and data stores
      - When employing tactics that depend on redundancy of functionality, the mapping from modules to redundant components is important.
        - For example, it is possible to write one module that contains code appropriate for both the acUve component and backup components in a protectton group.
- Resource Management
  - Determine what critical resources are necessary to continue operating in the presence of a fault: omission, crash, incorrect timing  or incorrect response.
    - Ensure there are sufficient remaining resources in the event of a fault to log the fault; notify appropriate entities (people or systems); disable the source of events causing the fault; be temporarily unavailable; fix or mask the fault/failure; operate normally, in startup, shutdown, repair mode, degraded operation, and overloaded operation
  - Determine the availability time for critfcal resources, what critical resources must be available during specified time intervals, time intervals during which the critical resources may be In a degraded mode, and repair time for critical resources.
    - Ensure that the critical resources are available during these time intervals
  - For example, ensure that input queues are large enough to buffer anticipated messages if a server fails so that the messages are not permanently lost
- Binding Time
  - Determine how and when architectural elements are bound.
    - If late binding is used to alternate between components that can themselves be sources of faul1s (e.g. processes, processors, communication channels)
    - ensure the chosen availability strategy is sufficient to cover fautts introduced by all sources. For example
      - a late binding is used to switch between artifacts such as processors that will receive or be the subject of faults, will the chosen fault detection and recovery mechanisms work for all possible bindings?
      - If late binding is used to change the definition or tolerance of what constitutes a fault {e.g. how long a process can go without responding before a fault is assumed) is the recovery strategy chosen suffident to handle all cases?
        - For example, if a fault is flagged after 0.1 milliseconds, but the recovery mechanism takes 1 .5 seconds to work, that might be an unacceptable mismatch.
      - What are the availability characteristics of the late binding mechanism itself? Can it fail?
- Choice of Technology
  - Determine the available technologies that can (help) detect faults, recover from faults, or reintroduce failed components.
  - Determine what technologies are available that help the response to a fault (e.g. event loggers).
  - Determine the availabllity characteristics of chosen technologies themselves:
    -  What faults can they recover from?
    - What faults might they introduce into the system?