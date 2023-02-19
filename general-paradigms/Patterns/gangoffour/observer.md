# Observer

## Implementation

- https://www.youtube.com/watch?v=_BpmfnqjgzQ

## Advantages

It supports the principle of loose coupling between objects that interact with each other
It allows sending data to other objects effectively without any change in the Subject or Observer classes
Observers can be added/removed at any point in time

## pitfalls

-  The Subject gets decoupled from Observer but you cannot just look at its source code and find out who observes it. Hardcoded dependencies are usually easier to read and think about but they are harder to modify and reuse. It's a tradeoff.
- All observers should be treated equally. IF not it breaks down. as events and interactions among objects become more complex, the assumption that observer equality becomes increasingly difficult to uphold. It is very tempting to just “hack” a few lines to get something work. Unfortunately, complexity will keep increasing, and a few lines of hack morph into nasty spaghetti code.
   - Complexity involves
    - Order of notification (e.g. Observer A must be notified before Observer B and C)
    - Conditional notification (e.g. Observer A only likes event X and Observer B only likes event Y).
    - Specialized notification (e.g. Create a event specialized just for Observer A)
- Cycles can be created, subject informs observer, which either informs something else which updates subject in a loop
- The Object to be observed knows who is observing (Subject<>--Observer). That is against real-life
- Due to shared interface of observers, they may not need all the information 

- https://askldjd.com/2010/03/18/pitfalls-of-observer-pattern/
