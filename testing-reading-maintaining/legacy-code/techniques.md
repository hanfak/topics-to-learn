# techniques

## Updating dependencies

## Exploratory Refactoring

## Documentation


## Mikado Method

- https://www.infoq.com/news/2012/02/mikado-method/
- https://youtu.be/9HmVrfkzm9I?t=1140 "Live Legacy Code Refactoring with the Golden Master" by Philippe Bourgau (@pbourgau)

## Testing

(move to new file)
- https://www.youtube.com/watch?v=cjxXv0eifhY Testing Legacy Code Elliotte by Rusty Harold
  - Give up 100% test coverage, but get some
    - You will not have perfect test coverage
    - But this is not a binary decision.
    - Some tests are better than none. More tests are better than fewer.
  - Give up 100% unit tests
    - Presumably the application is already working; at least mostly.
    - Broader tests work better for legacy code than narrow, unit tests
    - A broad test that covers a large swath of the application will help you notice if any of your changes break something.
    - Since you have finite time to spend writing tests, it is more important to get broad coverage than targeted coverage.
    - Of course, make sure anything you're changing is covered.
    - And anything you're adding can be done with test-first
  - Frequent context switches
    - Usually TDD writes just enough test code to make the tests fail; then writes model code only until all tests pass.
    - When working with legacy code, the model code is mostly already written.
    - Not uncommon to write a lot of tests before switching back to model code.
    - Actually we only give this one up in one direction; when adding new features we can use more traditional test driven approaches
  - Getting Started
    Write one test.
    It almost doesn't matter what it tests.
    Make it as broad as possible
    Automate it.
    This is a smoke test.
  - Testing main() method
    The main() method is sometimes a good place to start
    It's where the application expects to start
    It can reach into almost any part of the code
    Doesn't always work; many main() methods are not designed to be called more than once or from another main() method
  - Add fixtures
    After the first test is written, pull out any initialization and cleanup code into fixtures.
    Then think of as many other tests you can quickly and easily write based on these fixtures.
  - What Tests do you Already Have?
    Functional? Acceptance? System Integration?
    Standard conformance test suites (e.g. ANSI SQL, W3C XML)
    Manual test scripts
    Can you turn these into unit tests?
    Either automatically or manually?
  - Converting Existing Tests
    May need to mock out parts
    Probably need to subset the suite
    Maybe able to write one JUnit test that runs an en tire existign suite
    Later, break it into smaller units
  - Characterization Testing
    - Supply an initial bad expectation to a test to make sure it fails
      Use the actual value returned as the expectation for future runs of the test
  - Testing by Functional Division
    Fastest gains in code coverage come by starting your tests at the highest level.
    Look at what the application is doing, and write a test for each separate task.
    For instance, in a human resources application you might write one test each for:
      New hire,  Fire employee,   Generate payroll,  Schedule vacation, Raise salary, Change address etc.
    Notice that none of these have anything to do with how the code is structured. They don't even care what language the program is written in.
  - What to Test?
    Initially, focus on the main path of the application; not the edge conditions
    As the test suite expands, then you can start looking at the edge cases
    Even if you suspect or have diagnosed particular bugs, you still need tests for the main focus of the application.
    Remember: one of the main goals of this approach is to avoid accidentally breaking something when fixing a bug somewhere else.
  - Testing by Code Structure
    Not as important as testing by function
    A different way of organizing your thinking about the tests will dissect the application differently, cover different code, and reveal different things
  - Top Down
    One test per package/module
    org.jaxen.dom.html
    One test per class
    One test per method
    One test per line
  - Code Coverage Measurements?
    - How well are you doing?
    - More importantly, what have you missed?
  - Static Analysis
    - Don't neglect static analysis though. It will find real bugs you haven't noticed.
  - Test or debug?
    You will find bugs.
    Normally TDD stops testing and starts fixing when a bug is first noticed by the tests.
    But this assumes that you have tests for everything else in the model and can be fairly confident that you'll find out immediately if your fix breaks some other piece of the system.
  - How to decide
    Three questions
      Does the bug seem simple, obvious, and local?
      Do you understand the code where the bug appears?
      Do you understand the fix?
    If the answer to all three questions is yes, go ahead and fix the bug.
    If the answer is no, then you should probably expand the test suite first before fixing the code
  - Refactoring
    Much legacy code is not designed with testability in mind
    Refactoring can improve it so it's more testable
    Catch-22: Refactoring with confidence requires a good test suite
    All I can say is be careful.
    Most automated refactoring tools for Java at least are fairly reliable

### Approval tests

- Golden master
- charactisation testing

- Rely on logs/traces, to create an end to end test
  - Capture logs/traces (the output) and store it somewhere,
  - when changes are made, a new snap shot is created that is compared to the first snapshot, with the aim of no diff
  - can work with any side effects (I/o, network messages etc
- Should be short lived
- Not suitable for pipeline tests, not part of build


### Extract side effect code to protected then sub class and override in test


- Useful for
  - non injected dependencies, ie calls to static methods
  - static method calls to databases or http calls etc, which cannot be stubbed out (ie controlled)
- https://understandlegacycode.com/blog/quick-way-to-add-tests-when-code-does-side-effects/
