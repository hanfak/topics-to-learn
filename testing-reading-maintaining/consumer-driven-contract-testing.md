# consumer-driven contract testing

- Consumer-driven contracts are separated into a producer and consumers.
-  Consumer-driven contract testing verifies that the producer provides a contract that fulfils all consumers’ expectations.
- Consumers verify that the producers still provide the structure of messages and behavior they need.

## Contract testing

- A contract describes how components communicate and interact with each other, both message formats between components (syntax) as well as behavioral expectations of components (semantics).
- You use contract testing to verify that contracts between components are honored;
  - this gives you confidence that the components are able to work together
- When you use test-specific dependent components (such as test doubles), you can also use contract testing to make sure that they honor the latest or any specific version of the contract.



## PACTS

- https://docs.pact.io/
- https://github.com/DiUS/pact-workshop-jvm
- https://github.com/DiUS/pact-jvm
- https://www.javacodegeeks.com/2017/03/consumer-driven-testing-pact-spring-boot.html

## Spring consumer driven contracts

- https://www.javacodegeeks.com/2019/12/spring-covered-again-consumer-driven-contract-testing-messaging-continued.html
