# State Machines


## What 
- A state machine can be loosely defined as anything with a set of known states
- A system or process, where it can only be in one state at a time
- A collection of states, which when triggered by an event starts a transitions a state from the old state to a new state.
  - As part of this transitioning, actions can take place
- These events can be
  - Times/dates/timers will do something
  - incoming request to the system (http request, gui trigger)
  - Scheduled action
  - listening for some change somewhere (filesytem being updated, a queue)
- When in the new state, it can take some actions
  - ie store the state in the database, inform the user (request/gui update), validate next transition from event (is event legal)

## History 

- Comes from the idea of **Finite Automata** invented by McCulloch and Pitts in 1943
- Finite Automata consists of 
  - Finite set of states
  - Set of inputs
  - Initial State
  - Final State
  - Transition Function

## Why use

- In general, most code is a state machine, using 
    - multiple if -else
    - case/switch statements 
  - These can get messy and confusing, hard to debug with more states
- Using a FSM can help improve clarity of the flow from state to state
  - define consistent behavior for a finite number of states
  - Application logic is defined for specific states or state transitions
  - Application logic becomes more modular and more precisely defined

## Usage

-  Message (Event) based applications
- Events get published based on state changes
- UI Applications With Actions triggered by Use - Caps Lock On, Caps Lock Off
- Application behavior changes based on known states

## Terminology

- States - The specific state of the state machine. Finite and predetermined values. 
  - Frequently defined in an enumeration
- Events - Something that happens to the system - may or may not change the state. 
- Actions - The response of the State Machine to events. Can be changing variables, calling a method or changing to a different state 
  - Transitions - Type of action which changes state 
- Guards - Boolean conditions 
- Extended State - State Machine variables (in addition to state)



- https://medium.com/datadriveninvestor/state-machine-design-pattern-why-how-example-through-spring-state-machine-part-1-f13872d68c2d

## Examples

- https://github.com/shanwu/finite_state_machine/tree/master/FiniteStateMachine/src/main/java/FiniteStateMachine
- https://www.baeldung.com/java-enum-simple-state-machine
- https://blog.frankel.ch/builder-pattern-finite-state-machine/
- https://medium.com/datadriveninvestor/state-machine-design-pattern-part-2-state-pattern-vs-state-machine-3010dd0fcf28
- https://rclayton.silvrback.com/use-state-machines
- http://www.java2s.com/Code/Java/Collections-Data-Structure/AprogrammableFiniteStateMachineimplementation.htm
