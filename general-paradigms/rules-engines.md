# Rules Engines

## What?

- https://martinfowler.com/bliki/RulesEngine.html
- Instead of the usual imperative model, which consists of commands in sequence with conditionals and loops, a rules engine is based on a Production Rule System.
  - This is a set of production rules, each of which has a condition and an action - simplistically you can think of it as a bunch of if-then statements.
- The subtlety is that rules can be written in any order, the engine decides when to evaluate them using whatever order makes sense for it.
- A good way of thinking of it is that the system runs through all the rules, picks the ones for which the condition is true, and then evaluates the corresponding actions.

## How?

- You can build a simple rules engine yourself. All you need is to create a bunch of objects with conditions and actions, store them in a collection, and run through them to evaluate the conditions and execute the actions.

## Libraries

- https://github.com/j-easy/easy-rules
