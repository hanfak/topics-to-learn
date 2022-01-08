# Template

## What?

- A Template method pattern provides a skeleton for performing any sort of algorithm or an operation, and it allows the sub-classes to re-define part of the logic.
- Template Method uses inheritance to vary part of an algorithm
- Template Method modifies the logic of an entire class.
- Factory Method is a specialization of Template Method.

## When to use??

- When you want your program be "Open For Extension” and also “Closed for Modification”
- When you face many same line of codes that are duplicated through deferring just some steps of your algorithm.
- When you as a designer of a framework, want that your clients just to use any executable code that is passed as an argument to your framework, which is expected to call back (execute) that argument at a given time
- Natural fit for building frameworks, so that parent framework classes can make callbacks into methods implemented in child
- A template pattern should be used when there is an algorithm with many implementations

## Why use??

- Let subclasses implement varying behavior (through method overriding)
- Avoid duplication in the code , the general workflow structure is implemented once in the abstract class’s algorithm, and necessary variations are implemented in the subclasses.
- Control at what points subclassing is allowed. As opposed to a simple polymorphic override, where the base method would be entirely rewritten allowing radical change to the workflow, only the specific details of the workflow are allowed to change.

## Drawbacks

- Debugging and understanding the sequence of flow in the Template Method pattern can be confusing at times.
  - in other more complex scenarios state can be scattered throughout many (sub-) classes and source files that has to be managed and maintained somehow.
- instantiating objects to be able to call the methods is cumbersome. In general it is just an unwieldy construct.
- the abuse of the Template Method pattern tends to generate into deep hierarchies of concrete classes
  - Instead, Favor object composition over class inheritance
    - use Strategy pattern
-  A lot of boiler-plate code involved

## Links

- https://dzone.com/articles/template-method-pattern-revised
- https://sourcemaking.com/design_patterns/template_method
