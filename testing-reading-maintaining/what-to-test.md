# What to test

## General

- One behaviour per test
- Use table tests for multiple inputs and outputs
- Regression - so original behavour remains the same
- To break, when certain changes occur to think that it is correct choice
- Avoid repeating tests in other areas (not popular opinion)
- Aim for 100% test coverage
- Tests allows us to refactor/redesign the code, without changing the behaviour.
  - Safety net for changing the code with out breaking it

## What to test

Need to test behaviour
- if I call this method or hit this end point, what do i expect to happen,  depending on the state/setup of the system?

- Return value of method
  -
- Exceptions thrown
  - message
  - type of exception
  - stack trace is part of message
  - Cause of exception
- Return value us null
  - test dependencies are called (verify/spies), with inputs and how many times
  - use stubs in place of dependencies.
    - create extra methods in stubbed dependencies, used only in tests which return some value that can be asserted on.
  - ie logs
- Static methods
  - Change constructor to accept a supplier, while keeping original constructor
    - pass in stub as dependency which can be primed
  - might need to change production code
  - Allow static method to run if simple
- Dependencies which are called
  - Verify they are called, number of times and with correct arguments
    - ie logs
- Table / parametised  tests
  - Multiple cases for same flow

## Unit tests

- Test only the behavoir of one class
  - verify the behavior of a single unit, usually a class, while all concerns that are external to the unit are ignored or simulated.
  - test the business logic of the individual units, without verifying further integration or configuration thereof.
- All dependencies should be mocked
- Any tiny types/ domain types/ DTO/DAO etc, do not need to be mocked
- Test edge cases, technical issues
- fast feedback
- Issues
  - mocking the dependencies of the tested class means it is tightly coupled to the implementation, thus hard to refactor. As lots of changes need to be made to prod and test code

## Integration/module tests

- Bring up multiple classes, and mock a few.
- Test the integrations points, ie i/o, network, database etc

## End to End tests

- Bring the whole application app
- use test configuration/properties
- Testing outputs
  - return value of application
    - ie http response output - status code, body, headers
      - ie response body - test parts of json/xml which are important
- Testing changes to external IO
  - ie what is stored in the database/files
- Testing requests created to external dependencies
  - ie http request - headers, body, params, url
- Have logs shown in console and access to database, to help with debugging
  - logs should show request and response for entry point and dataprovider
- When debugging, not obvious where the issues can happen, and where to put breakpoints
  - good to show stack traces in logs
  - need to know how the flow of the application work (From entry point, to processing, to calling other dataproviders and auditing etc)
  -

## Static Analysis tests

- Using libraries like findbugs/pmd/pitest
- https://www.testingexcellence.com/static-analysis-vs-dynamic-analysis-software-testing/
- http://tryqa.com/what-is-static-analysis-tools-in-software-testing/
- http://ecomputernotes.com/software-engineering/what-is-static-analysis-how-is-it-performed-what-are-its-uses

## Acceptance/Documentation (end to end, integration or unit)

- Show in some output(ie webpage/file) the logs, the requests and responses, database info stored (ie object fields)
- If exposing unit tests, then cannot really show much output apart from the what was written in the tests or return value of method ie usecase performed.
- Regressiong testing
  - https://www.guru99.com/regression-testing.html
- Use BDD terminalogy
  - Given - for what is primed (dependencies - database has info, api called will return correct information, class dependency returns specific value etc)
  - When - The action performed (end point hit wiht body, or method called in body)
  - Then - Asserting on the key areas to show behaviour was done ( ie database has correct info, response for call has correct info, requests sent to internal requests are correct )
- Accpetance tests on classes (ie usecases - the main business area, or how the response is marshalled into json or how the request to dataprovder is marshalled etc)
  - These can show output, but mainly in object form. which may not make much sense to BA or testers
    - can format the output
  - Relying on the BDD wording of the test to show the situation being tested

## Black box tests

- Done mainly by testers/QA
- Have access to database, to check data
- Have access to log files, or see the log output of the app as it is processing the inputs
- Have a access to the output ie browser/postman
- Have access to stub (for external app calls) logs or output to see its interactions with app under test

## Acceptance/end to end or unit

- Doing ATDD means starting with a test which tests a whole flow (several modules). This means several classes might be created. But as these are already tested by acceptance test, you might not need to do a unit test on that class, because you will be duplicating tests and more things change later on.
- But if the class contains business logic or different flows ie handling resources or exceptions, which are not tested via the acceptance test then we need to unit test it.
  - If there is more business logic here then might need to write the unit test as a documentation test so it can be read by non technical stake holders.
- Dont just rely on the acceptance test to cover everything. Need to make a judgement on what needs to be unit tested and what needs to be documented

## Links

- https://blog.sebastian-daschner.com/entries/thoughts-on-efficient-testing
- https://phauer.com/2019/modern-best-practices-testing-java/
