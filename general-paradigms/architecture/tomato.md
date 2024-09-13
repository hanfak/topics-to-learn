# Tomato Architecture

## what

- Simplified hexagonal architecture
- Aim is to keep it simpler
  - Focus on separation of concern
    - package by feature
    - Keep app core/domain independent from delivery mechanisms
    - separate logic from input mechanisms
    - Dont let "External Service Integrations" influence the "Application Core" too much
    - Keep business logic in one place
  - Avoid unnecessary interfaces 
    - Dont expect to change things just in case you change technologies or delivery mechanisms or input sources
    - focus on changing the code instead of making it more abstract
  - Avoid keeping an indirection overt the framework, just in case of future change
  - Dont entirely focus on unit testing (ie mocking/stub out external dep or delivery mechanisms)
    - Aim to test these mechanism as a whole, as cheaper and faster to do
    - if not use something close to it, ie wiremock
- https://github.com/sivaprasadreddy/tomato-architecture
  - https://www.sivalabs.in/tomato-architecture-pragmatic-approach-to-software-design/

## Example

- JVM Performance Engineering

## Comparisons

- https://medium.com/oolooroo/navigating-the-maze-of-modern-architectures-comparing-and-contrasting-leading-software-dcec9b68fc87