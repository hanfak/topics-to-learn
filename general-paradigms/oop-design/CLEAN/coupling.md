# Coupling

- Aim to reduce coupling between objects.
- Cannot have no coupling.
-  the level of knowledge that one piece of code has about another piece of code that it is interacting with
- Can be either loose/weak or tight/strong
- Tight coupling means that one piece of code relies on the internal implementation details of code it collaborates with;
  - it uses knowledge of how the other code does something rather than just relying on it to do something.
- Loose coupling means that one piece of code does not rely upon, or even have knowledge of, the implementation details of the code it interacts with.
- keeping the relationship between objects intentional and clear
- code that is loosely coupled indirectly depends on the code it uses
- Can be achieved through use of an indirect call
  - Instead of calling a service directly (the concrete implementation of a class) it is called via an intermediary
  - Replacing the service will only affect the intermediary, reducing the impact of the change on the rest of the system.
- Should think in terms of intentional and accidental coupling
- Code has fewer side effects among entities, easier to test, reuse and extend
- If I have lots of unrelated dependencies, it is a coupling issue 

### Accidental coupling

- shows up when other code qualities are lacking
- EG If i have an uncohesive method that deals with many issues (has many responsibilities), I will have many unrelated reasons to couple with it.
- Avoid writing 'UBER apis'
  - they are fragile apis as they
    - try to do too much,
    - difficult to maintain and
    - couple code accross classes with that have no links to each other
  - IF different callers of an API share some of the same implementation or state for different reason, dont expose
  - ISP
    - create multiple apis that internally use only the part thats needed for each caller
- **Code reuse is good because it helps eliminate redundancy but at the expense of other code qualities**
-


### Intentional coupling

## Benefits of reducing coupling

- It make code simpler and more extensible. In the process, it provides insights on the details of the processing of a particular piece of data. It makes you learn a lot about the corresponding part of the program, both in terms of code and in terms of business features.
- changes in private, internal implementation details do not ripple throughout the rest of the system.
- Makes it easeir to isolate, verify, reuse and extend
- Lets you put *seams* in your code so you can inject dependencies instead of tightly coupling them
- This helps with make code more testable, by using the seam to replace the dependency with a stub/mock.

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
