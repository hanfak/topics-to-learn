# Service Locator

- The service locator pattern is different from dependency injection in the way the elements are consumed. With the service locator pattern, classes have control and ask for objects to be injected;
- Compared to dependency injection:
  - The collection of dependencies required by a service locator makes code harder to test because all the tests have to interact with the same global service locator.
  - Dependencies are encoded in the class implementation, not in the API surface. As a result, it's harder to know what a class needs from the outside. As a result, changes to Car or the dependencies available in the service locator might result in runtime or test failures by causing references to fail.
  - Managing lifetimes of objects is more difficult if you want to scope to anything other than the lifetime of the entire app.
- https://martinfowler.com/articles/injection.html
- https://www.baeldung.com/java-service-locator-pattern
- https://martinfowler.com/articles/injection.html#UsingAServiceLocator
-
