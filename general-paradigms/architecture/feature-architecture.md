# Feature Architecture

The code is organised by features of the application

```
src/main/java
├── CommonClass.java
├── aDomain
│   ├── aDomainValueType.java
│   ├── aDomainEntity.java
│   ├── aDomainUseCase.java
│   ├── aDomainServlet
│   └── aDomainDatabaseAdapter.java
├── anotherDomain
│   ├── anotherDomainAudit.java
│   ├── anotherDomainValueType.java
│   ├── anotherDomainEntity.java
│   ├── anotherDomainConfiguration.java
│   ├── anotherDomainTemplate.vm
│   ├── anotherDomainRequestUnmarshaller.java
│   ├── anotherDomainResponseMarshaller.java
│   └── anotherDomainResponseTemplate.vm
└── CommonException.java
```

- No layers
- All code relating to the feature is under one package
  - Easy to find all code related to this domain/service
- Can split out code duplication into a separate package or library
  - ie http client/ gateway, crosscutting code, webserver setup, database setup etc
- Use of package private within each feature package
- It is screaming
- We have no package names to identify our adapters, and we still don’t see the incoming and outgoing ports.
- we cannot use package-private visibility to protect the domain code from accidental dependencies to persistence code.
-  Since the infrastructure classes were in the same package and the core domain ones, it was hard to make sure that the dependencies pointed in the right direction.
