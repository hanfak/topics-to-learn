# Artifact repository

A place that will hold all the important files that will be used as part of the deployment of an application.

Such as

- application Jars
- properties
- docker images
- libraries jars

This can be on a server or cloud.

These are created as part of the CI and pushed to the server wheer the repository is held. When the deploying, we can grab the artifact when needed, and deploy it.

Similar to maven repository.

## Tech

- https://www.sonatype.com/product-nexus-repository
- https://mvnrepository.com/
- https://jfrog.com/artifactory/
- https://archiva.apache.org/

- For docker images
  - https://hub.docker.com/_/registry

## Links

- https://www.bogotobogo.com/DevOps/DevOps_Artifacts_Artifactory_Sonatype_Nexus_Maven_Artifact_Repository_Apache_Archiva.php
