# Layering & Dependency Inversion Principle

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Layering & Dependency Inversion Principle](#layering-dependency-inversion-principle)
	- [Moving into layers](#moving-into-layers)
	- [Layers Vs tiers](#layers-vs-tiers)
	- [Fowler: 3 Layers - Presentation, Domain, Data source](#fowler-3-layers-presentation-domain-data-source)
		- [Presentation](#presentation)
		- [Data Source](#data-source)
		- [Domain/business logic](#domainbusiness-logic)
		- [interaction](#interaction)
		- [When to layer](#when-to-layer)
		- [Dependencies](#dependencies)
		- [Where to run layers](#where-to-run-layers)

<!-- /TOC -->

## Moving into layers

- https://www.youtube.com/watch?v=v4dIcL0rVbs

## Layers Vs tiers

- tiers - physical seperation
  - client-server model is a two tier system
- Layers
  - Do not need to be seperated physically
  - Can all be on the same box or some seperate

## Fowler: 3 Layers - Presentation, Domain, Data source

Aim of having layers is to seperate coupling.

### Presentation

- Handling interaction between user of system and the system.
  - The entry points of the system
- is an external interface for a service your system offers to someone else, whether it be a complex human or a simple remote progra
- Examples
  - Command line
  - IOT
  - http (rest/soap) api (req/resp)
  - Files
  - Gui (desktop/html)
  - Scheduled jobs - quartz
  - handle user requests - keyboard/mouse/http req/file sent
- Responsibility
  - Display info to user
  - interpret commands from gui/request, and turn them into actions for the data source or domain to act upon (send messages to them)

### Data Source

- communicating with other systems that carry out tasks on behalf of the application
- is the interface to things that are providing a service to you
- Examples
  - transaction monitors
  - other applications - 3rd party apis
  - messaging systems - jms
  - Persistance - databases
  - Filesystems - ftp
- Responsibility
  - Handling all the details with interacting with these data sources

### Domain/business logic

- the work that this application needs to do for the domain you're working with.
  - What the process will do regardless of being software or a human doing it
- Examples
  - calculations based on inputs and stored data (Get from data source),
  - validation or changing of any data that comes in from the presentation,
  - figuring out exactly what data source logic to dispatch, depending on commands received from the presentation.

### interaction

Varys how they interact.

- Domain will only have access to data
  - Presentation <-> Domain <-> Data
- Presentation will get data and then pass it to data
  - Prestentation <-> Data
                  <-> Domain <-> Data

There can be multiple packages in each layer
- Two UI in presentation layer, ie http api and html gui

Each layer is talks to each other via interfaces

### When to layer

Depends on complexity. Small program, ie pulling data from datasource to display on command line, can be a one class but with layers split by methods. The more complex the more separation, from method to class to package to apps

### Dependencies

- Domain and Data should never be dependent on the presentation.
  - presentation can change, so should be able sub into app different presentation code (open/close principle)
- Should use DIP, have presentation implement interface, and domain and data depend on these interfaces
- Domain and Data interaction depends on architecture.
  - Generally use DIP
  - Logging can be an issue
- If changes in presentation, means changes in layers other than the presntation layer this is bad
  - If there's any functionality you have to duplicate in order to do this, that's a sign of where domain logic has leaked into the presentation. Similarly, do you have to duplicate logic to replace a relational database with an XML file?


### Where to run layers

- Better to run most processing on the server, rather than client (ie desktop/browser)
  - easier to upgrade and fix, no sync of different versions,
- On client
  - more responsive
    - no need to go to server
  - Not affected by being cut off from server, network is down
- What to split
  - Data is on the server
  - What functionality to duplicate on client and server??
    - Should data be cached on client in case of disconnect?
- Prestentation
  - Rich UI, ie desktops means presentation is on the client
  -
- Domain
  - either or split
  - IF split
    - to isolate this piece of logic in a self-contained module that isn't dependent on any other part of the system. That way you can run that module on the client or the serve
- Keep all codes in a single process, dont seperate layers into different processes
