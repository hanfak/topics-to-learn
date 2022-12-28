# Social Tests

Writing tests without using mocks/spies, but using stubbed out (test implementation of dependencies with possible extra logic or static factories in prod code used only for test), to test several classes at a time.

Thus allowing ease of refactoring, as code is not tied test implementation.

Test at high level

This is the idea behind unit tests (Bob martin, Khorikov)

- https://www.jamesshore.com/v2/projects/testing-without-mocks/testing-without-mocks
