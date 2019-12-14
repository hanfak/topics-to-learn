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
  - If testing integration part, ie db or network, the associated dependencies to allow for real implemenation must not be mocked but use the real object.

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
  - Can have a test database (ie test container) which mimics prod db
  - Used when method under test cannot be checked, so need to verify behaviour in a delegate that is called in the method. Thus can use a stub as a fake delegate  and assert on its state or methods.
  - Can have extra methods in stubs, which we can use to assert on
    - useful when method under test returns void, or want to check action has been performed by dependency (better to use verify with a mock)

- Using a lambda as a stub
  - https://dzone.com/articles/to-mock-to-stub-or-to-lambda

- Ways of priming time
  - Can apply to time or date
  - if test is using current time, ie Instant.now(), the code can not use the same current time, ie calling Instant.now() in prod code, as there will be time lag.
  - Solutions
    - Create an Interface, ie MyClock, with a one method, ie Instant getCurrentTime(). Pass this Interface as a dependency into

- Issues when priming
  - Mocked an object, primed it, but it does not look like it been primed during debugging
    - check the mocked class, is passed in as a dependency
    - While debugging, break point on test as well, note the object ref in test, it should be the same as the obj ref in the prod code.
