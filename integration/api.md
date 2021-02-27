# API

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [API](#api)
	- [What](#what)
	- [Types](#types)
	- [Code base](#code-base)
	- [Http](#http)
	- [Cosumner contract testing](#cosumner-contract-testing)
	- [Use of status probes](#use-of-status-probes)
	- [Best practices](#best-practices)
	- [Links](#links)
	- [Design](#design)
	- [Versioning](#versioning)
	- [REST](#rest)

<!-- /TOC -->

## What

- An interface, which defines how to use the service, and hides/abstracts the implementation
- are the basic building blocks for software as atoms and molecules are for matter in the physical world
- An API is an abstract specification about the basic functions provided for
building software that needs to use it.
- The software that provides the functionality described by an API is said to be an implementation of the API. An API implementation is presented to users as a part of a software development kit (SDK). An SDK contains not only the implementation of an API, but also the documents and code samples about how to use the APIs.
- Access paths to APIs must be specified when calling programs are compiled
and built.
- An API is different from an ABI (application binary interface)
	- An API defines the interface between source code and libraries so that the same source code will compile on any system supporting that API
	- ABI allows compiled object code to function without changes on any system using a compatible ABI.
- API providers (backend developers) should do everything in their power to reduce the work done by the clients of their APIs
	- Having APIs created by backend developers without clearly understanding the needs of the their clients and respective flows lead to complex delivery mechanisms and frictions between teams

## Types

- Operating system api
	- Allows access to the services provided by os and hardware
- Language api
	- set of api provided by a language (a set of libraries) that allows the user to access common higher level functions (i/o, string manipulations, data structures) to create complex software
	- Reduces need to recreate these common functions, allows other more experienced people to create them to reduce bugs and improve performance
- Internal code api
	- This is a part of your software, using another part of your software (ie method, function, instance/static method, constructors etc)
	- Not splitting code into separate services/api etc makes it harder to code as complexity sets in
	- Design does not matter much for small or if it is single person working on it
		- but when it gets big, multiple people working on it, people leaving it, then thought needs to be taken care and should have apis similar to language/library apis (those of high standards)
- First party api
	- generally libraries or programs access over network produced by the same programmer, team, department or company
- Third party api
	- eg google api
	- generally libraries or programs access over network produced by another company or opensource
	- Can pay for it's usage to get better access/performance/support
- Company-private APIs
	- Only used by systems controlled by the API provider (internal)
- Public APIs
	- Used by systems not controlled by the API provider (external)
- Hybrid APIs
	-  Used by internal and external systems

## Code base

- Defined by an interface, which defines the method's signature (name of method, params, return type)
- When using a library, which is external and cannot change, need to follow it's api
  - Should wrap it in an adapter/facade to avoid core application logic from being too dependent on it. Can now change it in one place with out changes in the api affecting it's usage in the application
-

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

## Best practices

- https://completedeveloperpodcast.com/episode-162/

## Links

- https://www.mulesoft.com/resources/api/types-of-apis

## Design
- As they are not in our control (although can monkey patch or take over if opensource) they affect the performance of the software that depends on them
	- So changes in version, can have an impact on the software's
		- performance
		- compilation can break
		- creation of code (learn new api or it's changes)
	- If paid service is not renewed or service breaks legal/regulations than it needs to be removed and replaced,
		-  which will slow down creation of features of software
		-  need to retune to match previous performance
-  Need of good naming
-  Use of conventions
- https://swagger.io/blog/api-development/how-to-build-an-api/
- https://dzone.com/articles/7-tips-for-building-an-api
- https://github.com/dwyl/learn-api-design

## Versioning

- https://github.com/dwyl/learn-api-design

## REST
