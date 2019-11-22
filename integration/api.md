# API

- An interface, which defines how to use the service, and hides/abstracts the implementation


## Code base

- Defined by an interface, which defines the method's signature (name of method, params, return type)
- When using a library, which is external and cannot change, need to follow it's api
  - Should wrap it in an adapter/facade to avoid core application logic from being too dependent on it. Can now change it in one place with out changes in the api affecting it's usage in the application

## Http

- Having an exposed endpoint, the users may not be able to change their code to call the new endpoint. So need to maintain this contract.
- Use of flags/version in api address, so the producer can create the new end point and the consumer can use or switch over to it when they want to
- May want a new endpoint to expose, but need to add some mapping to the old (or about to be decomissioned) endpoint, as no time to fully get rid of it.

## Cosumner contract testing

- Makes sure api is consistent between internal services/apps
- Allows checking of the api and what it expects matches both what the producer and consumer expects
- Libraries such as PACTs
- Good for usuage in pipeline
  - Check when a build is created from either producer or consumer to check if api has changed
  - Check when new version of producer or consumer is being deployed to an environment that it matches what is already in an environment. This stops the deployment if there is a mismatch, and work might need to be done in either the consumer or producer.

## Use of status probes

- Can have a system which constently checks the api is correct, by making an OPTIONS or test call, to check whether a 3rd party api is still working. This can give some quick feedback to implement the changes
- Any change in an external api, should have been warned about before it is deployed, so work can be done to consume it.
- The producer should have versioning in api to allow consumers to be able to switch over

## Links

- https://www.mulesoft.com/resources/api/types-of-apis

## Design

- https://swagger.io/blog/api-development/how-to-build-an-api/
- https://dzone.com/articles/7-tips-for-building-an-api
- https://github.com/dwyl/learn-api-design

## Versioning

- https://github.com/dwyl/learn-api-design

## REST
