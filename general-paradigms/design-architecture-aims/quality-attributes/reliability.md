# Reliability

The system should continue to work correctly (performing the correct function at the desired level of performance) even in the face of adversity (hardware or soft‐ ware faults, and even human error).

Expectations of a reliable system:

- The application performs the function that the user expected.
- It can tolerate the user making mistakes or using the software in unexpected ways.
- Its performance is good enough for the required use case, under the expected load and data volume.
- The system prevents any unauthorized access and abuse.
- It still works if there is a hardware fault

Reliability = continuing to work correctly, even when things go wrong

faults: The things that can go wrong. as one com‐ ponent of the system deviating from its spec

fault tolerent / resliant: systems that anticipate faults and can cope with them

- Cannot cope with all faults. Need to be specific.

failure: when the system as a whole stops providing the required service to the user.

Aim is to design fault-tolerance mechanisms that prevent faults from causing failures.

To test fault tolerant systems, need to push it to limits, by to increase the rate of faults by triggering them deliberately. Use of netflix chaos monkey.

generally prefer tolerating faults over preventing faults.

Better to prevent than cure, if no cure exist.

## Hardware faults

Very common. Being random and independent from each other, weak correlation that one fault leads to another.

Examples:

- Hard disks crash
- RAM becomes faulty
- the power grid has a blackout
- someone unplugs the wrong network cable

Solutions:

- add redundancy to the individual hardware compo‐ nents in order to reduce the failure rate of the system
- Redundancy: When one component dies, the redundant component can take its place while the broken com‐ ponent is replaced.
- To keep machine running interrupted
- multi-machine redundancy was only for applications for which high availability was absolutely essential.


  Examples

  - Disks may be set up in a RAID configuration
  - servers may have dual power supplies
  - hot-swappable CPUs
  - datacenters may have batteries and diesel generators for backup power

- Aim: For systems that can tolerate the loss of entire machines, by using software fault-tolerance techniques in preference or in addition to hardware redundancy.
- Increased loads in data and computing demands of the systems, requires more machine and more faults can occur. Thus toleranting these faults if a machine goes down is essential
- a single-server system requires planned downtime if you need to reboot the machine
- a system that can tolerate machine failure can be patched one node at a time, without downtime of the entire system
  - Doing a rolling upgrade

## Software Errors

systematic error within the system. Harder to anticpate, cause more failures. Cascading failures.

Lie dormant, until triggered by unsual acts.

Prevent:

- carefully thinking about assumptions and interactions in the system
- thorough testing; process isolation
- allowing processes to crash and restart
- measuring, monitoring, and analyzing system behavior in production
- Self guarantee, by checking itself while running and alerting when a discrepancy is found.

## Human Errors

Humans design and build software systems, and the operators who keep the systems running are also human.

humans are known to be unreliable

Solutions:

- Design systems in a way that minimizes opportunities for error.
  - well-designed abstractions, APIs, and admin interfaces
  - if the interfaces are too restrictive people will work around them, negating their benefit, so this is a tricky balance to get right.
- Decouple the places where people make the most mistakes from the places where they can cause failures.
  - provide fully featured non-production sandbox environments where people can explore and experiment safely, using real data, without affecting real users.
- Test thoroughly at all levels, from unit tests to whole-system integration tests and manual tests
- Allow quick and easy recovery from human errors, to minimize the impact in the case of a failure
  - make it fast to roll back configuration changes
  - roll out new code gradually
  - provide tools to recompute data
-  Set up detailed and clear monitoring
  - performance metrics and error rates
  - telemetry is essential for tracking what is happening, and for understanding failures
  - metrics can be invaluable in diagnosing the issue
- Implement good management practices and training

Why care about reliability?

- lost productivity
- legal risks if figures are reported incorrectly
- outages of ecommerce sites can have huge costs in terms of lost revenue and damage to reputation

Sacrifice reliability will reduce costs, development and operational. For prototyping

## Links

- shirazi https://youtu.be/KoIabbk_gsg
  - https://medium.com/expedia-group-tech/the-cost-of-100-reliability-ecb2901f23a4
