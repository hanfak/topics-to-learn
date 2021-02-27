# Libraries

- Callng code from other code sources that are not your own, is integrating a dependency into your application.
  - Calling a method in a library that has been imported on to the classpath, is similar to calling a http api endpoint

## Benefits

- Reduce writing code over and over again
- Faster response than http call over network, if doing the same thing, as there is network latency
  - although depends if that library calls something over the network (ie it is a client for a service)
- Dependable, as a http service might be down or slow network, but the library is shipped with your code so will always be there
- Algorithms used can be far more efficient and correct than yours, thus reducing time for creating this to spend on app specific code
- Maintains a specific way of doing something

## Downsides

- Need to wait for others to update, if there are issues or you need a new feature, or you did it and waiting for it to be added to new version
- Need to manage the versions, issues with transitive dependencies
  - Use of build tools like maven/gradle helps
- If a new version is out, you need to manually update yourself
  - Can have plugins in maven to check for latest
- Can get locked in to libraries if not careful
  - use of clean architecture/ DIP and being very sure that it is necessary for key areas of code base
- Can be massive libraries where you used a few things, leads to code bloat
  - Can copy and paste the code
  - monkey patch
- May need to adapt the code to meet your needs, this can lead to ownership of code (time to learn etc)
- Issues with open source libraries, not maintained, does not meet company polices etc

## Creating libraries

check curl library

- Modularise – make the library single purpose
- Ensure that the consumers are local
- Document it well, as though it’s a larger library
- Stop before it gets too diverse/entangled
- Avoid putting service business logic into the library

## Links

https://www.javacodegeeks.com/2020/04/the-library-paradox.html
