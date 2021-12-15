# Best Practices

- don't treat them as traditional servers.
  - ie  you might be tempted to update your application inside of a running container, or to patch a running container when vulnerabilities arise.
- Containers are designed to be stateless and immutable.
  - This combination allows you to automate deployments and increase their frequency and reliability.

## Statelessness

- Stateless means that any state (persistent data of any kind) is stored outside of a container. This external storage can take several forms, depending on what you need:
  - To store files
  - To store information such as user sessions, using an external, low-latency, key-value store, such as Redis or Memcached.
  - If you need block-level storage (for databases, for example), you can use an external disk attached to the container.
- By using these options, you remove the data from the container itself, meaning that the container can be cleanly shut down and destroyed at any time without fear of data loss. If a new container is created to replace the old one, you just connect the new container to the same datastore or bind it to the same disk.

## Immutability

- Immutable means that a container won't be modified during its life:
  -  no updates, no patches, no configuration changes.
- If you must update the application code or apply a patch, you build a new image and redeploy it.
- Immutability makes deployments safer and more repeatable.
- If you need to roll back, you simply redeploy the old image.
- This approach allows you to deploy the same container image in every one of your environments, making them as identical as possible.
- To use the same container image across different environments, we recommend that you externalize the container configuration (listening port, runtime options, and so on).
  - Containers are usually configured with environment variables or configuration files mounted on a specific path.
  -  In Kubernetes, you can use both Secrets and ConfigMaps to inject configurations in containers as environment variables or files.
- If you need to update a configuration, deploy a new container (based on the same image), with the updated configuration.

## Avoid privileged containers

- In a virtual machine or a bare-metal server, you avoid running your applications with the root user for a simple reason:
  - if the application is compromised, an attacker would have full access to the server.
- For the same reason, avoid using privileged containers.
  - A privileged container is a container that has access to all the devices of the host machine, bypassing almost all the security features of containers.
- If you believe that you need to use privileged containers, consider the following alternatives:
  - Give specific capabilities to the container through the securityContext option of Kubernetes or the --cap-add flag of Docker. The Docker documentation lists both the capabilities enabled by default and the ones that you must explicitly enable.
  - If your application must modify the host settings in order to run, modify those settings either in a sidecar container or in an init container.
    - Unlike your application, those containers don't need to be exposed to either internal or external traffic, making them more isolated.
  - If you need to modify sysctls in Kubernetes, use the dedicated annotation.
- In Kubernetes, privileged containers can be forbidden by a specific Pod Security Policy.

## Avoid running as root

- Containers provide isolation:
  - with default settings, a process inside a Docker container cannot access information from the host machine or from the other collocated containers.
- However, because containers share the kernel of the host machine, the isolation isn't as complete as it is with virtual machines.
  - An attacker could find yet unknown vulnerabilities (either in Docker or the Linux kernel itself) that would allow the attacker to escape from a container.
  - If the attacker does find a vulnerability and your process is running as root inside the container, they would get root access to the host machine.
- To avoid this possibility, it is a best practice to not run processes as root inside containers. You can enforce this behavior in Kubernetes by using a PodSecurityPolicy.
- If you want to avoid running as root, design your container so that it can be run with an unknown, non-privileged user. This practice often means that you have to tweak permissions on various folders.
- if you are following the single application per container best practice and you are running a single application with a single user—preferably not root, you can grant all users write permissions to the folders and files that need to be written in, and make all the other folders and files only writable by root.
- If your container needs an external volume, you can configure the fsGroup Kubernetes option to give ownership of this volume to a specific Linux group. This configuration solves the problem of the ownership of external files.
- If your process is run by a non-privileged user, it will not be able to bind to ports below 1024. This is usually not an issue, because you can configure Kubernetes Services to route traffic from one port to another. For example, you can configure an HTTP server to bind to port 8080 and redirect the traffic from port 80 with a Kubernetes Service.


## Best Practices for building images

- https://cloud.google.com/solutions/best-practices-for-building-containers#package_a_single_app_per_container
- https://docs.docker.com/develop/develop-images/dockerfile_best-practices/
