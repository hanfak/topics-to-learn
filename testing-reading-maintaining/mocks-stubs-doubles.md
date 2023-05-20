# Mocks, Stubs & Doubles


## What
- Mocking is used for protocol testing - it tests how you'll use an API, and how you'll react when the API reacts accordingly.
- Ideally (in many cases at least), that API should be specified as an interface rather than a class - an interface defines a protocol, a class defines at least part of an implementation.
- Test doubles turn integration tests into unit/isolation tests

- https://8thlight.com/blog/uncle-bob/2014/05/14/TheLittleMocker.html
- https://martinfowler.com/articles/mocksArentStubs.html
- https://javacodehouse.com/blog/mockito-tutorial/
- https://www.codurance.com/publications/2019/04/08/introduction-to-test-doubles
- http://xunitpatterns.com/Mocks,%20Fakes,%20Stubs%20and%20Dummies.html

## mockito

- https://stackoverflow.com/questions/22867680/how-does-mockito-mock-interfaces
- https://www.toptal.com/java/a-guide-to-everyday-mockito

## mocks

- Cannot mock final class/methods using mockito 1.x, need latest version (use inline dependency)

### How to control final classes

- If class is final but in your scope of change
  - Add an interface to the class to be controlled, and create a test class that implements that interface, then inject it into the system under test
- If class is final but not in your scope of change
  - Cannot add an interface
  - Can wrap the dependency (adapter), replace the call of the actual with the adapter in codebase and mock the adapter in the tests

### How to verify non injected objects

- When a object is instantiated in the class under test, and want to verify that this object is used, we can use argumentcaptor
- Thus when we it is used (we check the captor is used in the mehtod we verify) then can grab use the object that was captured, use its method and assert on them

### Links
- https://stackoverflow.com/questions/10598898/mockito-numberformat-mocking-nullpointer-in-when-method


## stubs

- provide canned answers to calls made during the test, usually not responding at all to anything outside what's programmed in for the test
- Stubbing is the process of giving behavior to a function that otherwise has no behavior on its own—you specify to the function exactly what values to return (that is, you stub the return values).
- ie From mockito: when(...).thenReturn(...)
- typically done through mocking frameworks
- stubbing is appropriate when you need a function to return a specific value to get the system under test into a certain state
- each stubbed function should have a direct relationship with the test’s assertions.
-  real implementations or fakes are still preferred because they don’t expose implementation details and they give you more guarantees about the correctness of the code compared to stubbing
### Limitations


## Dummy
- are passed around but never actually used. Usually they are just used to fill parameter lists.

## Spy

- are stubs that also record some information based on how they were called. One form of this might be an email service that records how many messages it was sent.

## Fakes

- A fake is a lightweight implementation of an API that behaves similar to the real implementation but isn’t suitable for production
- for example, an inmemory database, wiremock
- Using a fake is often the ideal technique when you need to use a test double, but a fake might not exist for an object you need to use in a test, and writing one can be challenging because you need to ensure that it has similar behavior to the real implementation, now and in the future
- Normally use an already written on
  - otherwise it is hard to create, as it must mimic the real implementation and must be maintained

## Mocks
- are pre-programmed with expectations which form a specification of the calls they are expected to receive. They can throw an exception if they receive a call they don't expect and are checked during verification to ensure they got all the calls they were expecting

## Interaction Testing

-  is a way to validate how a function is called without actually calling the implementation of the function. A test should fail if afunction isn’t called the correct way; for example, if the function isn’t called at all, it’s called too many times, or it’s called with the wrong arguments.
- interaction testing is typically done through mocking frameworks
- Interaction testing is sometimes called mocking
- it is preferred to test code through state testing
-  it can only validate that certain functions are called as expected. It requires you to make an assumption about the behavior of the code; for example, “If database.save(item) is called, we assume the item will be saved to the database."
- Leaks details to test
- when to use
  - You cannot perform state testing because you are unable to use a real implementation or a fake
  - Differences in the number or order of calls to a function would cause undesired behavior
  - PREFER TO PERFORM INTERACTION TESTING ONLY FOR STATE-CHANGING FUNCTIONS
  - you should perform interaction testing only for functions that are state-changing

### With state testing
- you call the system under test and validate that either the correct value was returned or that some other state in the system under test was properly changed
- it actually validates this assumption (such as by saving an item to a database and then querying the database to validate that the item exists)
- if cannot state, use interaction testing, but also use integration testing

## London/mockist school
## chicago/classic school

## Mocking frameworks

- A mocking framework is a software library that makes it easier to create test doubles within tests;
  - it allows you to replace an object with a mock, which is a test double whose behavior is specified inline in a test.
- The use of mocking frameworks reduces boilerplate because you don’t need to define a new class each time you need a test double.

## why
- Essential for testing and not want to call anything which can have consequences (ie state change (internally or externally), production calls, charges for services)
-  If you want to verify the behavior of the system under test (SUT), using mockito can be more effective as it allows you to verify interactions between the SUT and its collaborators.


## Problems with mocking


- When you mock something you’re removing all confidence in the integration between what you’re testing and what’s being mocked.
  - You will need to do separate tests for integration part, to see that it actually works
- mocking is somewhat overused - often you're not really interested in the exact interaction, you really want a stub... but mocking framework can be used to create stubs, and you fall into the trap of creating brittle tests by mocking instead of stubbing. It's a hard balance to get right though.
- When using verify (to check a dependency has been called) this ties the test to the implementation/structure of the code, rather than the behaviour
  - better to have stub injected, and assert on the stub
  - dependencies are part of the constructor and thus public
- Can lead to mocking everything except the SUT
  - This can make test brittle
  - SUT is not necessarily a class, but can be a bunch of objects to test the behaviour
  - Over-reliance on mocks can lead to tests that are not representative of the real-world behavior of the system, resulting in tests that are less effective and less reliable.
- SUT with lots of dependencies and interactions, and use of mocks can make tests more complex and unclear with lots of extra code
- Leaks implementation details into your test
  - Ideally, a good test should need to change only if user-facing behavior of an API changes; it should remain unaffected by changes to the API’s implementation
- Use of mocking frameworks can lead to false sense of security
  - MAke tests hard to maintain
  - makes refactoring harder, as tests will break
  - bug finding hard
- test doubles, does not have exact sameness as the real implementation, so always some form of security that it is give correct evaluations
- https://engineering.talkdesk.com/double-trouble-why-we-decided-against-mocking-498c915bbe1c
- https://youtu.be/7AGQ9dhWCX0 Test Doubles Are A Scam – Matt Diephouse
- Mocking can add additional processing time during the build process, slowing down the overall build time.


### alternative - use real implementations

- makes refactoring easier
- known as classical testing
- tests are more realistic, more confidence in the system
- Using real implementations can cause your test to fail if there is a bug in the real implementation.
  - A real implementation is preferred if it is fast, deterministic, and has simple dependencies. For example, a real implementation should be used for a value  object
  - for more complex code, using a real implementation often isn’t feasible
    - ie database or network calls, edge of app. these can be mocked
    - ie for nondeterministic code  such as external servers, time, randommness
- Can be slow
- Need to construct the object graph for the SUT, can be complex
  - Should use the same mechanism as test, and adjust (ie factories) to replace mocked dependencies

### alternative - use fake implementations

- Instead of a real implementation, use an inmemory version
- This a fake or stub 
- If there is a logic which mimics the actual impl in the fake, it needs to be tested to ensure it matches the real impl and be used with accuracy in the tests

### Links 

- https://medium.com/javascript-scene/mocking-is-a-code-smell-944a70c90a6a
- https://chemaclass.medium.com/to-mock-or-not-to-mock-af995072b22e

## Mocking third party

- This should not be done, should avoid mocking third party code
- https://youtu.be/v6hP2MXoVrI Don't Mock 3rd Party Code

- 