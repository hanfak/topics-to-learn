# Libraries

- These are jars that are used in other java applications.
- A Java library is Java-virtual-machine-based bytecode which encodes the classes in the library.
- A library is shared via a "jar" file (essentially just a zip file of the classes) and, once it is referenced in your classpath is available to be invoked by other classes (including from other libraries).

## Creating a library

- Using gradle
  - https://guides.gradle.org/building-java-libraries/
- Using maven

### deploying to a artifact repository

- Examples of artifact repository
  - mvn repository
  - jfrog artifactory

## Using a library

- Via dependency management tool ie mavan, gradle
- Downloading the jar, and adding it to the class path manually

## Monkey patching

- Not advised
- You can augment an existing class. You can add methods and attributes.
- You can modify a method of an existing class.

### Links

- https://www.beyondjava.net/what-about-monkey-patching-is-it-as-dangerous-as-they-say

## Design

- https://www.oracle.com/corporate/features/library-in-java-best-practices.html
