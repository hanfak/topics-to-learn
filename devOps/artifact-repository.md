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
