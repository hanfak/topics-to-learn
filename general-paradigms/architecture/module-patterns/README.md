# Modularity

- A principle of software engineering.
- specialization of the principle of separation of concerns
- separating software into components according to functionality and responsibility

## What

- A module:
  - has a codebase that is separate from other modules’ code,
  - is transformed into a separate artifact (JAR file) during a build, and
  - can define dependencies to other modules or third-party libraries.
- A module is a codebase that can be maintained and built separately from other modules’ codebases.
  - a module is still part of a parent build process that builds all modules of our application and combines them to a single artifact like a WAR file.

## Why?

- Strong encapsulation — The access-control mechanism of the Java programming language and the Java virtual machine provides no way for a component to prevent other components from accessing its internal packages. The proposed specification will allow a component to declare which of its packages are accessible by other components, and which are not.
- a single monolithic codebase is susceptible to architectural decay.
  - Within a codebase, we usually use packages to demarcate architectural boundaries.
  - But packages in Java aren’t very good at protecting those boundaries.
  - Suffice it to say that the dependencies between classes within a single monolithic codebase tend to quickly degrade into a big ball of mud.
  - If we split up the codebase into multiple smaller modules that each has clearly defined dependencies to other modules, we take a big step towards an easily maintainable codebase.


## Types of Modules

- Relating to Java
- Types
  - Maven modules are a way to organize your project into several subprojects (modules). With Maven, you can control the versions of these modules and the dependencies between these modules. Each module will produce an artifact.
  - Java modules are a way to strongly encapsulate your classes. It does not provide any means to control the version of an artifact you are using.
  - ntelliJ also uses the term module. It is a way to group files
  - 
