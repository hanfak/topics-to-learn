# Gateway pattern

- encapsulates access to an external system or resource
- A gateway class provides a simplified way of interacting with something external that perhaps has a peculiar or difficult API.
- A gateway class can be created to facilitate interaction with this external system
- keep software soft by abstracting and insulating the system being developed from its external dependencies
- By also defining an interface for the gateway, it makes it possible to provide fake versions for testing purposes or swap out one third-party address validation service for another without the change rippling throughout the system.
- The gateway also helps to deal with anything unique to the external service
