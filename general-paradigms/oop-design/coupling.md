# Coupling

- Aim to reduce coupling between objects.
- Cannot have no coupling.
-  the level of knowledge that one piece of code has about another piece of code that it is interacting with
- Can be either loose/weak or tight/strong
- Tight coupling means that one piece of code relies on the internal implementation details of code it collaborates with;
  - it uses knowledge of how the other code does something rather than just relying on it to do something.
- Loose coupling means that one piece of code does not rely upon, or even have knowledge of, the implementation details of the code it interacts with.

## Benefits of reducing coupling

- It make code simpler and more extensible. In the process, it provides insights on the details of the processing of a particular piece of data. It makes you learn a lot about the corresponding part of the program, both in terms of code and in terms of business features.
- changes in private, internal implementation details do not ripple throughout the rest of the system.

## Examples

- A function remains coupled with another object because it accesses its data (via getters and setters)


- https://codurance.com/software-creation/2016/07/25/thoughts-on-coupling-in-software-design/
- https://martinfowler.com/ieeeSoftware/coupling.pdf

# Law of Demeter (LoD)

- known as Principle of Least Knowledge
- talk only to your friends, not to strangers.
  - it is ok to make reference to immediate collaborators (“friends”) from a piece of code, but not the collaborators (strangers) of those collaborators.
- Reduces coupling
- when dealing with views (xml/json) it can be acceptable to reach into strangers’ data in order to display it.
- is it data or behaviour that is being wrapped/”delegated”. If it is behaviour then it can often be a better candidate for applying LoD than data.
