# Assertions

- Assertions are removed at runtime unless you explicitly specify to "enable assertions" when compiling your code.

## Use

- they're designed for development-time testing and debugging because they cost nothing if assertions are disabled in production. I think it's better to create explicit tests in your testing framework (e.g. a unit test for edge conditions) than rely on someone enabling assertions while testing.
- The purpose of assertions are to catch bugs. You should only use them where the only way to "handle" them is to go back and fix the code
- assert can be used to verify pre conditions, invariants and post conditions during integration and testing phases. This helps to catch the errors while in development and testing phases. And you can safely turn it off in production to avoid performance issues.

## Links

- https://www.baeldung.com/java-assert
- https://docs.oracle.com/javase/6/docs/technotes/guides/language/assert.html#design-faq
