# Mocks, Stubs & Doubles

- https://8thlight.com/blog/uncle-bob/2014/05/14/TheLittleMocker.html
- https://martinfowler.com/articles/mocksArentStubs.html
- https://javacodehouse.com/blog/mockito-tutorial/
- https://www.codurance.com/publications/2019/04/08/introduction-to-test-doubles

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
## Doubles
## Spy
## Fakes
## London/mockist school
## chicago/classic school


## Problems with mocking

- Essential for unit testing
- Essential for testing and not want to call anything which can have consequences (ie state change (internally or externally), production calls, charges for services)
- When you mock something you’re removing all confidence in the integration between what you’re testing and what’s being mocked.
