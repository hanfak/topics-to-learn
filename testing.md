# Testing

Testing is baked into everything I do. We write test first and have testers do checks on our applications.

## Methodologies

* Test Driven Development (TDD)
  * starting with unit test to drive development
  * For unit tests
  * Test behaviour not methods
  * Process: Red - Green - Refactor
    * RED - Failing test
      * ie expected this got something else
    * GREEN - Pass test
      * Write production code to make test pass
    * REFACTOR - Tidy up code
      * i.e. better designed, better performant
  * No production code with tests
  * Have mutation test code coverage (ie [Pi test](http://pitest.org/)) to check all production code is covered by tests
* Acceptance Test Driven Development (ATDD)
  * Starting with acceptance test to drive code development
    * Red - Green - Refactor
  * Yatspec (java library)
    * Allows to have readable output for non technical people (ie html and in english)
    * Can Draw sequence diagrams ( use plantUML) show interactions between different apps
    * Table tests available
  * Syntax: Given - When - then
    * Given: setup dependecies ie databases/3rd party apis
      * Use of Wiremock to stub 3rd party apis
      * Use of test database instead of production or a stub
    * When: Run the application, and interact with it ie make a request to end point
    * Then: Assertions, assert on output of request, database changes, verify apis called
      * Use of Junit and matching libraries ie hamcrest/assertj
  * AKA Behaviour Driven Development (BDD)
* Testing pyramid

## Types of Tests

### White Box Testing

Types of test

* Acceptance Tests - testing features of apps
  * Whole app run, testing visible outputs
  * Visible for testers and Business to check that code does what it wants in less technical language but in business language
  * Stubbing out other dependencies
* Documentation tests - Having visible tests for business functionallity at unit level exposed
  *
* Module test
* unit tests
  * Avoid using static methods as cannot mock and might be expensive to use (ie long test times, use resources)
* Static Analysis Tests - testing the code it self not the Behaviour
  * findbugs
  * code style (PMD)
  * code coverage
    * line (Intellj)
    * mutation (Pitest)
* Consumer driven contract testing (PACT tests)
  * test apis between internal services used between apps
  * Useful for microservices
* Learning Tests
* Smoke/confidence Tests
* Performance tests
*

### Black Box Testing

* Component testing
  * Manual testing of application where other apps are stubbed (using stubbing application)
* Use of postman application, to send requests to api
* Use of selenium to test front end  guide
* Integration testing
  * Have all dependencies up and running and not using a stub
* Release testing
* Testing in different environments in the pipeline

## Stubs

- used in component testing, but mocking out other dependencies through this
- bottom up
  - have app up but stub mocks all dependencies
- Top down
  - stub represents app and mocks responses from it instead
- Storing state, ie as files
- priming stub
- using stub
- Wiremock

## mockito

* Mock
* Verify
* When...ThenReturn...
* Dummy

## Junit

- asserting
  - boolean
  - exception thrown
  - expected == actual
  - collection matchers
- Before
- After
- Ignore
- Setups
  - in tests
  - outside of test
- @Note

## yatspec

* Captured inputs and outputs
* combining with Wiremock
* linking note
  * link test to classes or other tests
* Interesting givens
  * any important domain information set in the givens
* test state


## Writing Tests

* Arrange - Act - Assert - Teardown
  * Order in test method
  * Arrange can be put in a before block or start of test
  * Teardown can be put in an after block
  * Arrange include
    * Mocking other dependecies in class and/or return values if dependency's methods are called
      * Use Mockito
    * Starting up other parts of the app ie database or new up classes
  * Asserting on output of code
    * verifying methods of dependencies have been called
      * mockito
    * Asserting on output
      * Junit and AssertJ


## links

* Wiremock
* Yatspec
* AssertJ
* Junit
* Mockito
*
