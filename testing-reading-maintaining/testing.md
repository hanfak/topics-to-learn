# Testing

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Testing](#testing)
	- [What are tests](#what-are-tests)
	- [Why write tests](#why-write-tests)
	- [Test harness and Test frameworks](#test-harness-tand-test-frameworks)
	- [Methodologies](#methodologies)
	- [Test Driven Development (TDD)](#test-driven-development-tdd)
	- [Acceptance Test Driven Development (ATDD)](#acceptance-test-driven-development-atdd)
	- [Testing pyramid](#testing-pyramid)
	- [Trophy Pyramid](#trophy-pyramid)
	- [Links](#links)
	- [Types of Tests](#types-of-tests)
		- [White Box Testing](#white-box-testing)
	- [Builds](#builds)
	- [Making code more testable](#making-code-more-testable)
		- [Black Box Testing](#black-box-testing)
	- [Stubs](#stubs)
	- [mockito](#mockito)
	- [Junit](#junit)
		- [AssertJ](#assertj)
	- [yatspec](#yatspec)
	- [Writing Tests](#writing-tests)
	- [links](#links)

<!-- /TOC -->

Testing is baked into everything I do. We write test first and have testers do checks on our applications.

## What are tests

- Make sure code does what it is meant to do

## Why write tests

- Give us confidence in system
- Prevent bugs, spot bugs early, reduce costs
- Document behaviour (business flows), show examples of how system works
- Enforce coding behaviour (architecture, styles)
- Allows for refactoring, by allowing changes and know if they break the behaviour
- If a bug or something unexpected happened, a test will prevent this from happenning again
- No manually checking code yourself
- A set of tests can be used in CI to check that system does what it is supposed to do, and that version can be used to be deployed
- As a reminder to be sure you want to make that change
- If wanting to refactor a code, writing all possible tests to check all behaviour has been documented first then can refactor it

## Test harness and Test frameworks

- Test harness can be explained as a unit testing tool that helps in the automation and execution of unit test cases.
	- It enables the automation of unit tests for any software application
- Advantages of test harness
	- helps to automate the overall testing process to the maximum extent.
	- capable to execute test suites which are composed of multiple test cases.
	- capable to generate test report either by its own as in case of TestNG or through another third party tool or development as in the case of Junit.
	- composed of drivers and stubs which are small programs, therefore, they are capable to Support debugging of code.
	-  tools can capture the test results for an entire suite as well as individual test present inside the suite or standalone test.
	- helps developers in the early identification of a defect at the code
	- enables developers to measure the code coverage at code or elementary level during application development.
	- helpful in terms of increasing the system productivity through the test automation
	- enhance the quality of software components or overall software application
	- help to cover complex test scenarios which are very difficult to handle through tradition testing approach.
	- adds confidence to the organization marketing team towards the robustness of the application software as it is well tested right at unit level.
- Disdavantages of test harness
	- tools do not support record and play features.
	- Testers using test harness tools are expected to have knowledge of programming languages
	- it incurs a cost for writing automates test suites or test cases through skilled developers.
- Where test harness is used
	- Automation testing:
		- developers develop test scripts
		- test scripts require test data along with setting up of certain test parameters which are necessary to execute the automation test scripts
		- After these test scripts are executed, the test results are captured and analyzed in the form of test reports.
	- Integration testing:
		- the two modules within the same application or different applications are integrated and testing is conducted to make sure both modules which are developed separately are working smoothly as a single unit when integrated.
		- test cases are written and executed as automation script or through tools such as Junit
		- results are recorded as a report and analyzed for exit criteria of the overall integration testing to be successful.
- Example of test harness
	- Junit: It is an API written in JAVA language which is used to design and implement test cases to conduct the unit testing for JAVA program or JAVA based applications. They are very frequently used to test applications which are built in JAVA language.
- Test Automation framewokr
	- a set of procedures, processes, intellectual concept and environment through which the tester can design and implement automated tests.
	- composed of information such as the test library, automated testing, testing tools, best practices, and testing platform
	- It allows tester can manually “Record & Playback” script in this framework
	- categorized into
		- Data-driven testing
		-  Modularity driven testing
		- Hybrid testing
		- Code driven testing
		- module driven testing
		- behavior driven testing
		- Keyword driven testing.
	- Exmaples
		- Cucumber, Robot Framework, etc
		- yatspec

## Methodologies

## Test Driven Development (TDD)

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

## Acceptance Test Driven Development (ATDD)

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

## Testing pyramid

* More resource expensive and time consuming tests at the top (few of them). Cover less, but make sure everything fits and works together.
* More unit tests, less expensive, mocked/stubbed, fast running tests at the bottom. Cover more of the code base.

- https://blog.ncrunch.net/post/testing-pyramid-automated-testing.aspx

## Trophy Pyramid

<img src="testing-trophy.png" alt="testing-trophy.png" width="700">

- ROI is better to have more integration tests, than unit tests.
  - Int tests cost more and slower than unit tests. But need to write more unit tests, to match one Int test
- Rely on static typing and compiler to handle syntax and language errors
  - use of static analysis tools
  - Dont test business logic
- Unit tests
  - to test edge cases
- Integration tests
  - to handle business flows or integration points ie database, http calls
  - test multiple areas at once
  - make sure that parts of system work together
  - Less mocking, more real objects used
- End to End test
  - Bring up whole app, test user flows
  - critical paths
  - little to no mocking, some for services dont want to use
- Integration and end to end can be very fuzzy demarcation
- Reduce duplication of tests, if unit is tested via Integration or end to end test, it does not need to be retested
  - Makes code more brittle, more places to change code
- If test does something that your consumer of that code doesnt then it's testing implementation details
- If refactor breaks your tests, then it's testing implementation details

## Links

- https://blog.usejournal.com/lean-testing-or-why-unit-tests-are-worse-than-you-think-b6500139a009
- https://kentcdodds.com/blog/write-tests

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
  * links
    * Sandi metz https://www.youtube.com/watch?v=URSWYvyc42M
* Static Analysis Tests - testing the code it self not the Behaviour
  * findbugs
    * https://self-learning-java-tutorial.blogspot.co.uk/2018/03/a-short-tutorial-on-findbugs.html
    * http://findbugs.sourceforge.net/
  * code style (PMD)
  * code coverage
    * line (Intellj)
    * mutation (Pitest)
* Consumer driven contract testing (PACT tests)
  * test apis between internal services used between apps
  * Useful for microservices
* Learning Tests
  * http://tomhesl.in/learning-tests/
  * Use of tests to learn and document open source libraries
  * Use of test to find out if library should be used
* Smoke/confidence Tests
* Performance tests
*

## Builds

- Run all Tests
- flickery tests


## Making code more testable

- need to extract out any dependecies, especially those that are being newed up in the class under test (so they can be mocked)
-
### Black Box Testing

* Component testing
  * Manual testing of application where other apps are stubbed (using stubbing application)
* Use of postman application, to send requests to api
* Use of selenium to test front end  guide
* Integration testing
  * Have all dependencies up and running and not using a stub
* Release testing
* Testing in different environments in the pipeline
* Smoke Tests
  * Run actual workflow, and see if works (something that does not affect other services but does some interal business logic)

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
* Argument captors

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
- Fuzzy assertions

### AssertJ

- Readbility and intent via fluent api
- Extracting
- Soft Assertions
	- https://joel-costigliola.github.io/assertj/core/api/org/assertj/core/api/SoftAssertions.html

## yatspec

* Acceptance Tests
* BDD language
* Captured inputs and outputs
* combining with Wiremock
* linking note
  * link test to classes or other tests
* Interesting givens
  * any important domain information set in the givens
	* givens state
* test state
* state extractors
* given builders
* action under test
* Sequence diagrams
* Dictionary
* Linking notes
* html output
* parametised/table  tests



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

- https://mixandgo.com/learn/feature-tests-vs-integration-tests-vs-unit-tests-in-ruby-and-rails
- https://testing.googleblog.com/2008/12/static-methods-are-death-to-testability.html
- http://misko.hevery.com/code-reviewers-guide/
- https://blog.sebastian-daschner.com/entries/thoughts-on-efficient-testing
- Google testing blog: https://testing.googleblog.com/search/label/TotT
- automation test (UI) https://ultimateqa.com/automation-patterns-antipatterns

* Wiremock
* Yatspec
* AssertJ
  * https://dzone.com/articles/fluent-assertions-with-assertj
  * http://joel-costigliola.github.io/assertj/index.html
* Junit
* Mockito
*
