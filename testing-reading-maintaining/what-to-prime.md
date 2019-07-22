# What to prime

To test anything, need to setup the conditions to test that situation/behaviour

- Unit tests
  - dependencies (injected classes)
    - ie io/3rd party/ http/jms/database
    - use stubs (fake objects)
    - use mocking frameworks
  - static methods

- module tests (integration tests)
  - Some dependencies need not be primed
    - ie io/3rd party/ http/jms/database

- End to End tests
  - use stubs to return value for external dependencies
    - ie apps it talks to over http
    - use a stub app, ie small app that app under test can talk to
      - will need to instantiate when bringing app up for the test
  - Use test database instead of production
    - if simple use a stub
    - use in memory database
    - use test container


- clearing primed data
  -  Otherwise other tests will have primed data/http responses not for that situation
