# Usecases

- Also known as
  - Services
  - Application
- These should be thin, one usecase class per business flow
  - Avoids broad and fat Usecases
  - Easier to find
  - Simpler to test
  - Reduce amount of dependencies
- All dependencies from outer layers (databases, 3rd party, ui etc) shoul point toward the use cases
  - Thus interfaces should be in the same package/module as the usecase
  - Easier to mock out these dependencies
  - Use case only changes when business rules change, rather than infrastructure does
- Can model domain how we want
  - ie domain driven design
