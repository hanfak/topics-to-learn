# Software Designed
Software design is the only tool that we have to try to constrain entropy.

Computers are state machines. There is a wide variety of state transitions that are permitted by the computer, the set of allowable state transitions is the instruction set. The number of possible states and the number of possible state transitions is each so large that both of them are effectively infinite. In other words, the system is unconstrained. The unconstrained nature of the machine makes it a very powerful tool because it can be used to represent a very wide variety of problems. However, for a specific problem only a vanishingly small number of machine states is valid. A bug causes the system transition to a random invalid state (random in the sense that the bug can cause any state transition allowed by the instruction set). Over time, bugs move the state of the system further and further toward the most common states and away from the small number of valid states. In other words, bugs raise the entropy of the system state. Software design puts rules in place that constrain the allowable state transitions to a set small enough for a human to understand. Having such constraints makes the problem easier to understand and also makes bugs (violations of the constraints) easier to identify and understand.

From this I define Sofware Design (as a verb) to fundamentally be the process of creating a set of constraints that serve to reduce the scope of the problem within a given context by restricting the set of valid state transitions available to the software developer.

- https://medium.com/@aboutcoding/forgotten-tenets-for-effective-software-design-ae0ec1413806

## Software Design desicions

### Generic vs. Specific Solutions:
- Generic Solutions: Designed for flexibility and reuse across multiple scenarios, but they introduce coupling, which can make changes more complex and interconnected.
- Specific Solutions: Tailored for a particular problem or context, often simpler to implement initially but might lead to duplicated code.

### Coupling and Cohesion:
- Low coupling (independence between components) is desirable, while high cohesion (related components working closely together) is beneficial. Generic solutions often increase coupling.
Code Reuse and Duplication:

### DRY Principle: 
- "Don't Repeat Yourself" suggests avoiding code duplication.
- However, duplication isn't harmful until changes are needed.
- Rule of Three: 
- Copy code as needed, and only abstract it on the third instance to avoid premature or incorrect abstractions.
### Design Considerations:
- YAGNI Principle: "You Aren't Gonna Need It"
  - avoid overengineering solutions that may not be needed.
- Five W’s: When proposing generic solutions, ask "why" repeatedly to validate the need for generalization.
- Cost of Generic Solutions: Consider the effort required for generic solutions versus specific ones. Generic solutions are often more complex and expensive.

### Organizational Impact:
- Conway's Law: Design systems should align with the organizational structure.
  - Forcing a generic solution in a misaligned organization can fail.
- Cost and Complexity: Building reusable components can be three times as challenging as single-use components. Assess the long-term benefits against immediate costs.

### When to Go Generic:
- Valid reasons include anticipated broad use, complex logic or skills, or the need for encapsulation to shield complexity.
- Avoid going generic based on bad reasons like tradition, resistance to libraries, or unsubstantiated future-proofing.

A well-designed system should balance between flexibility and simplicity. A program that’s easy to change is more valuable in the long run than one that’s inflexible but works perfectly.