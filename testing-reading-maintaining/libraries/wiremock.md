# Wiremock

- https://examples.javacodegeeks.com/software-development/use-wiremock-for-mocking/
- https://semaphoreci.com/community/tutorials/restful-integration-testing-with-wiremock-in-java
- https://github.com/vladimir-dejanovic/wiremock-examples

## Why use?

- If using a library that makes http calls under the hood, you can write a test with wiremock intercepting the url.
  - This will help you find the request which is sent
    - This is useful if you need to prime (say stub for manual testing) response to look for a specific request
    - Assert in acceptance/end to end tests that the client made the correct request
- Can use to create stub application, to bring up while component testing your application
  - This way you have control of priming responses dependent on matching different parts of the incoming request
  - Can use a scenario build, to match on same request, but have different response
  - One place to prime multiple applications that interact with your application under test
  - If app interacts with a non http producer (ie telnet), you can create a proxy side car, which starts a server (ie telnet server) that mimics productions, which then talks to a stub which can be easily primed
- Useful for writing tests, to prime the givens (ie what is expected to be returned from service)
- If dont want to create a stub, can use wiremock docker instance and a wiremock chrome extension
