# What to prime

To test anything, need to setup the conditions to test that situation/behaviour

- mock/stub classes which you are in control of and will create or can change

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
  - before each test, good to remove data from database
    - avoid doing after test, as it is good to have data there if test failed to help in debugging

- Avoid mocking third party classes
  - Cannot make assumptions of such classes
  - Use a module test or end to end test, use the actual object instead

- Using a stub
  - Allows to use polymorphism to create a replacement dependency which mimics the prod dependecy as well as provide methods only for testing
  - It is dumb, but fast
  - Generally used for database or network calls classes, for acceptance tests
  - Can replace a network call without going over the network, or go other network to a local server which returns whatever you want (wiremock)
