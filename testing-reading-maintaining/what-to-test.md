# What to test

## General

- One behaviour per test
- Use table tests for multiple inputs and outputs

## Unit tests

- Return value of method
- Exceptions thrown
  - message
  - type of exception
  - stack trace is part of message
- Return value us null
  - test dependencies are called (verify/spies), with inputs and how many times
  - use stubs in place of dependencies.
    - create extra methods used in tests only which return some value that can be tested
- Static methods
  - Change constructor to accept a supplier, while keeping original constructor
    - pass in stub as dependency which can be primed
  - might need to change production code
  - Allow static method to run if simple

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

## Acceptance/Documentation (end to end, integration or unit)

- Show in some output(ie http/file) the logs, the requests and responses, database info stored (ie object fields)

## Black box tests

- Have access to database, to check data
- Have access to log files, or see the log output of the app as it is processing the inputs
- Have a access to the output ie browser/postman
- Have access to stub (for external app calls) logs or output to see its interactions with app under test
