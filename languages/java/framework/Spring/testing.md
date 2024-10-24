# Testing

## Smoke tests

- spring generally creates a starter app with a single spring boot test that has a context load method
- This is useful as it brings up the app, and checks for any dependency injection issues
- Can take time

## web mvc test

- To test the controller layer
  - generally mock the delegates 
  - Can inject other classes that handle any controller stuff (ie convertors, unmarshallers, exception handlers etc)
- Seen as a unit test, so should be in the same package as the controller
  - if want to move need to set the component scan to the class where the main method is
- Use of mockmvc

## Spring boot test

- To test the whole app, end to end flow
- The app is brought up, the whole object graph created and properties used
- Can use RestTemplate to send http requests to the controller and retrieve the response to assert on
- Generally slower
- Assert on what the user sees, ie responses, messages sent to queue, logs, database state etc
- Messages send or consuming
  - https://www.baeldung.com/spring-jms-testing

### Links 

- https://rieckpil.de/guide-to-springboottest-for-spring-boot-integration-tests/

## Spring extension

- Can be used as part of junit5, to set up some configuration (prod and test) to test some part of the code base (ie several classes)
- https://rieckpil.de/what-the-heck-is-the-springextension-used-for/
## JPA/Database tests 

## Test containers
- https://www.youtube.com/watch?v=erp-7MCK5BU  Spring Boot Testcontainers - Integration Testing made easy!

## Integration tests
- https://www.baeldung.com/spring-tests 

## Http clients 
## Links 

- https://youtu.be/2bTAb-2vhBk  Learnings From Netflix To Effective Testing With Spring Boot (SpringOne 2024) 
- https://rieckpil.de/start-here/
  - https://www.youtube.com/watch?v=hR0bbk2tsF0  Things I Wish I Knew When I Started Testing Spring Boot Applications by Philip Riecks @ Spring I/O 
- https://www.youtube.com/watch?v=rUbjV3VY1DI  Spring Boot Testing - ** Batteries Included 🔋🔋 
- https://www.youtube.com/watch?v=u5foQULTxHM  Spring Boot testing: Zero to Hero by Daniel Garnier-Moiroux
- https://docs.spring.io/spring-framework/reference/testing.html
  - https://spring.io/guides/gs/testing-web
- https://www.lambdatest.com/blog/spring-testing/
- https://www.baeldung.com/spring-boot-testing