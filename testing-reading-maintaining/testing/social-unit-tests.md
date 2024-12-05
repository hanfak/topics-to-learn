# Social Tests

## What
- Also known as
    - documentation tests
    - acceptance unit tests
    - module tests
- test that verifies the behavior of a unit (e.g., a class or a function) in collaboration with its real dependencies rather than mocking them
    - Any infrastructure calls (ie http, message bus, files etc) are stubbed/faked out
- Writing tests without using mocks/spies, but using stubbed out (test implementation of dependencies with possible extra logic or static factories in prod code used only for test), to test several classes at a time.
- Used in testing the core of hexagonal architecture
    - With business rules being tested
    - with the ports implementing fakes
    - Adapters not tested
- Avoiding use of mocks to verify
    - as these are dealt with ....????
    - 
- Care about the output
    - ie the reponse
- This is a testing pattern, and not a hammer
  - should be have reasons to use, and use other tests type
## Characteristics
- Real Collaborators: The unit interacts with its actual dependencies.
- Integration-Like: Tests a small part of the system, often a subset of the domain or application logic, an aggregate
- Behavior-Oriented: Focuses on the outcome of the collaboration rather than internal implementation details.
- Limited Scope: While broader than solitary tests, they do not span the entire application stack (e.g., they exclude the database or external systems).

# Advantages

- Thus allowing ease of refactoring, as code is not tied test implementation.
- validate the actual collaboration between multiple units, rather than have fine grained tests
- When testing the business logic in a domain-driven design or hexagonal architecture, sociable tests ensure domain entities and value objects work together correctly. 
  - Example: An aggregate root interacting with child entities to enforce invariants.
- Good for handling complex interactions.
  - When interactions between multiple components are too complex to mock effectively without missing edge cases or creating brittle tests.
  - Example: Validating the flow of a process where components communicate heavily (e.g., an order placement pipeline).
- Avoiding Mocking Overhead:
  - Sociable tests are beneficial when mocking dependencies would introduce unnecessary complexity or make the test fragile.
  - Example: A calculator service that depends on multiple reusable utility classes.
- Avoid testing implementation, and focus on testing behaviour
- Focused on business rules:
  - avoid testing situations that will never happen in a business flow, 
  - example: as the calling object calling it might never have the state that could be used in the test.
  - Can be used with BDD language and be read by business
- Avoid mocking/stubbing business rules that might return the wrong thing
- Less end to end acceptance tests


## Disadvantages/When not to use
- Testing Behavior with External Systems or boundaries:
  - Avoid sociable tests for interactions with databases, file systems, network APIs, or other external systems.
  - This is integration tests
- Highly Independent Units:
  - If a unit has minimal or no interaction with other components, a solitary unit test is sufficient. 
    - Example: Testing a string utility function or a pure algorithm.
- Complex algorithms/rules:
  - Can start off with a social test, but might be easier to unit test the rules/algorithm separately and easier (ie remove dependency graph)
- Non-Deterministic Behavior:
  - unsuitable for systems with non-deterministic behavior (e.g., random number generation, time-based behavior) unless the randomness can be controlled. 
  - Example: A test that depends on real-world timing or randomness.
- Complex Dependency Graphs
  - hen the dependency graph is too complex, as this can lead to brittle and slow tests. 
  - Example: A service relying on many indirect dependencies through deeply nested calls.
  - This can be handled via a factory
- Performance Concerns:
  - Can be slow due to complex setups or large numbers of interacting components, they may not be ideal for fast feedback loops.
- Can be harder to isolate failures
  - When multiple units are involved, it can be difficult to pinpoint which unit is causing a test failure.
  - Will need to use a debugger more
- Limited Fault Injection
  - It’s harder to simulate specific edge cases or failure scenarios compared to solitary tests with mocks or stubs.
  - Example: Testing how a service handles an exception from a dependency may require significant effort to trigger that failure
- Overlap with Integration Tests
  - may duplicate the purpose of integration tests, leading to redundancy and wasted effort.
- Reduced Control Over Dependencies
  - use real dependencies, which means they lack the fine-grained control provided by mocks or fakes.
  -  A dependency that randomly changes its state (e.g., based on system time) might cause sporadic test failures.
  - Real dependencies may introduce non-determinism (e.g., caching, threading, random inputs), making tests unreliable.
- Potential Over-Reliance
  - Overusing sociable tests can lead to insufficient solitary unit tests, which are crucial for pinpointing issues within individual units.
  - 
## Examples

## Links

- https://www.jamesshore.com/v2/projects/testing-without-mocks/testing-without-mocks
