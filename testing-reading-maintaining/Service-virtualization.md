# Service-virtualization and api mocking

- is also called API simulation or an API mock.
- It is the practice of replacing real dependent components with test versions created using powerful service-virtualization tools.
- Service-virtualization tools allow a simulator-like experience but with less effort from developers and testers.
- Instead of building a custom test double per dependency, off-the-shelf tools take care of the boilerplate functionality that is common across typical handwritten implementations.
- Service-virtualization tools generally offer more features than stubs or mocks, like recording requests and responses or built-in support for multiple technologies like HTTP, JMS, FTP, or gRPC.
- Test without relying on the real service
- Test in hypothetical or hard to test scenarios
- Test more scenarios with less efforts
- Simulators are called virtual services

## why use

- Reduce costs
  - complexity
  - time to market
  - risk
- shift left , accelerate delivery
  - dev teams can work in parallel
  - test teams detect defects early
- simulate the dependencies
  - simulate test env
  - reduce infrastructure costs
  - remove bottle necks
  - less manual test data management
- automate sooner
  - create automated suites of tests with less effort
- simulate third party
  - reduce interaction with third party
  - reduce costs
- more agile
  - decouple other teams and systems  

## Benefits

- unblocking testers and devs waiting for APIs
- easier and faster to reproduce bugs in prod
- speed up setting up test data
- eliminate the need for scheduling time on env
- reduce third party transaction costs
- performance tests become more reliable
- automated builds run faster

## Creating virtual services

- recording traffic and replaying it when systems is intereacting with it
- creating manually
  - using documentations and examples
- importing from logs
- generating from schemas ie swagger, open api

## What can you do

- test systems without relying on dependent components
- setting up test data
- simulating api Errors
- simulate protocol specific errors
- simulate slow responses 
