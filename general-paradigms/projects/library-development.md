# Library development

- creating a jar/binary to use within other application, to provide some functionality
- The user/consumer, can use the functionality how they see fit
- This involves creating an API
  - A set of method signatures (method name, return type, inputs) as contracts that the use can use
    - This can include constructors, thus constructors need to be thought about too
  - This can lead to coupling, so changes to these api can break users

## Design considerations

### Backwards compatibility


### Versioning

- semantic

### Tests

- To check it works
- To see how it works
  - Documented tests
  - example tests

### Documentation

- Java docs
- wiki/readme

## Access to library

- Best to use a build (maven/gradle) and CI to create the binary, and push it to the repository
- local
  - create jar, and add to class path
- Allow users to create it locally
- Create it and push it to a private/public repository (artifactory, maven, jitpack etc)
  - If paid, create and give it to them so they can add it
