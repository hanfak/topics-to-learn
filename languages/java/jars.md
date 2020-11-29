# Artifacts, Jars

- To run an app in production, we need the app to published as an artifact that can be deployed in productions servers (ie cloud etc)
- Applications of any use normally use libraries outside the jdk, this means for the app to run the libraries (modules, java classes) need to be on the class path, so the application can find them when they are imported into the class
- Having lots of libraries can make your jar massive, and building the jar takes up time (especially on a CI server)
- But most dependencies are the same and rarely change, yet to build a new version of the jar, you have to redownload all the dependencies to create the jar.
- The use of fat jars were useful, as it allowed the containerisation of the application ( and it needed all the libaries on the classpath) but were massive (think about the upload/download time and cost of storing the artifact/jar/image in a repository)
  - The old school way, allowed us to use the skinny jar (containing only the application classes) as the libraries were already loaded on the servers
- This has led to teams to go back to using skinny jars in the microservice world
  - https://product.hubspot.com/blog/the-fault-in-our-jars-why-we-stopped-building-fat-jars
  - Where to artifacts were built and uploaded (the app and dependencies)
