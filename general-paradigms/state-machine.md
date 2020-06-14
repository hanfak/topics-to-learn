
- A system or process, where it can only be in one state at a time
- A collection of states, which when triggered by an event starts a transitions a state from the old state to a new state.
- These events can be
  - Times/dates/timers will do something
  - incoming request to the system (http request, gui trigger)
  - Scheduled action
  - listening for some change somewhere (filesytem being updated, a queue)
- When in the new state, it will take some actions
  - ie store the state in the database, inform the user (request/gui update), validate next transition from event (is event legal)



- https://medium.com/datadriveninvestor/state-machine-design-pattern-why-how-example-through-spring-state-machine-part-1-f13872d68c2d

## Examples

- https://github.com/shanwu/finite_state_machine/tree/master/FiniteStateMachine/src/main/java/FiniteStateMachine
- https://www.baeldung.com/java-enum-simple-state-machine
- https://blog.frankel.ch/builder-pattern-finite-state-machine/
- https://medium.com/datadriveninvestor/state-machine-design-pattern-part-2-state-pattern-vs-state-machine-3010dd0fcf28
- https://rclayton.silvrback.com/use-state-machines
- http://www.java2s.com/Code/Java/Collections-Data-Structure/AprogrammableFiniteStateMachineimplementation.htm
