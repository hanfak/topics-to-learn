# Acceptance tests

- Documents the key uses of the app
  - using html/wiki with key info
  - such as ????
- Used in end to end and unit tests
- Help understand how the system works, from business pov
  - if tests written by devs, it will also show how the app works as well
- Explain domain of the app
- Run as another stage
  - modularised and run after unit tests
  - needs jar of app to run
- Need to run in CI, create documentation in location that is accesible

## Parts

- Follows the 3 A and T (Arrange, Act, Assert and Teardown)

### Given

- This is the Arrange part
- Here we set the state of the system/app to test the scenario
  - Priming the state
- Similar to how we mock the dependencies in unit tests
- What we will generally prime
  - response from application calls to services (http/jms etc)
  - Database/files state
  - Times and dates
- Things that you prime, will not be asserted on
- We will use things that will help stub the response that we primed
  - ie wiremock, stub classes,
- Or we will use live services which are used for testing
  - some internal apps, or use specific id/tokens/requests for tests
- Or use mimiced services
  - like test databases or test containers, which are are exactly like prod

### When

- This is the Act part
- Where your application is up and running, and you send a request or use the system in some way
  - ie http request to some end point
- Generally we are interested in knowing about the what the app returns and any state that has changed (files/Database)
  - We will generally look to store this for later use (ie asserting on)
- To make a request, we will either use some sort of client to do this, so as to automate rather than act as the user
  - ie http client, selenium

## Thens

## Teardowns

## Links

- https://youtu.be/7CZitmD_R58Acceptance Testing Sounds Easy, But Is Hard To Get Right - Peter Gfader
