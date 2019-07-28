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

## Unit tests

- Test only the behavoir of one class
- All dependencies should be mocked
- Any tiny types/ domain types/ DTO/DAO etc, do not need to be mocked
- Test edge cases, technical issues

## What to test

- Return value of method
- Exceptions thrown
  - message
  - type of exception
  - stack trace is part of message
  - Cause of exception
- Return value us null
  - test dependencies are called (verify/spies), with inputs and how many times
  - use stubs in place of dependencies.
    - create extra methods used in tests only which return some value that can be tested
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

- Show in some output(ie http/file) the logs, the requests and responses, database info stored (ie object fields)
- If exposing unit tests, then cannot really show much output apart from the what was written in the tests
- Regressiong testing
  - https://www.guru99.com/regression-testing.html
- Use BDD terminalogy
  - Given - for what is primed (dependencies - database has info, api called will return correct information, class dependency returns specific value etc)
  - When - The action performed (end point hit wiht body, or method called in body)
  - Then - Asserting on the key areas to show behaviour was done ( ie database has correct info, response for call has correct info, requests sent to internal requests are correct )
- Accpetance tests on classes (ie usecases - the main business area, or how the response is marshalled into json or how the request to dataprovder is marshalled etc)
  - These can show output, but mainly in object form. which may not make much sense to BA or testers
  - Relying on the BDD wording of the test to show the situation being tested

## Black box tests

- Done mainly by testers/QA
- Have access to database, to check data
- Have access to log files, or see the log output of the app as it is processing the inputs
- Have a access to the output ie browser/postman
- Have access to stub (for external app calls) logs or output to see its interactions with app under test
