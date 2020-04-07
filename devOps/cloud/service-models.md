# Service Models

## Types

Typical services offered by cloud vendors

### Infrastructure as a service (IaaS)

- in which users have direct, on-demand access to virtual machines, as well as a suite of related services to automate common tasks.
- Unmanaged services that provide virtual machines
  - the system provides a robust computing infrastructure, but you must choose and configure the platform components that you want to use.
  - the cloud provider will ensure that resources are available, reliable, and ready for you to use, but it's up to you to provision and manage them.
  - The advantage here is that you have complete control of the systems and unlimited flexibility.

### Platform as a service (PaaS)

- in which the machine layer is abstracted away completely, and users interact with resources by using high-level services and APIs.
- A cloud provider handles most of the management of the resources for you.
  - For example,
    - if your application requires more computing resources because traffic to your website increases, the cloud provider automatically scales the system to provide those resources.
    - If the system software needs a security update, that's handled automatically
- Capabilities
  - Build your app in several languages and use pre-configured runtimes, or use custom runtimes to write code in any language.
  - managed app hosting, scaling, monitoring, and infrastructure
  - Connect with the cloud storage services.
    - RDMS, nosql
  - Use the cloud's security servcies to identify security vulnerabilities as a complement to your existing secure design and development processes.
  - Use cloud monitoring, logging and other features

### Functions as a service (FaaS)

- a serverless computing model that allows you to run individual functions in response to a variety of triggers.
- you write simple, single-purpose functions that are attached to events raised by your cloud infrastructure and services.
- Your Cloud Function runs when a watched event is raised. Your code executes in a fully managed environment; you don't need to provision any infrastructure or worry about managing any servers.
- Examples
  - Data processing and ETL operations, for scenarios such as video transcoding and IoT streaming data.
  - Webhooks to respond to HTTP triggers.
  - Lightweight APIs that compose loosely coupled logic into applications.
  - Mobile backend functions.

### Containers as a service (CaaS),

- an IaaS/PaaS hybrid that abstracts away the machine layer but retains much of the flexibility of the IaaS model.
- you can focus on your application code, instead of on deployments and integration into hosting environments
  - is built on the open source Kubernetes (or other container management  systems) system, which gives you the flexibility of on-premises or hybrid clouds
- Features
  - Create and manage groups of instances running Kubernetes, called clusters. Where each node runs the Docker runtime, a Kubernetes node agent that monitors the health of the node, and a simple network proxy.
  - Declare the requirements for your Docker containers by creating a simple JSON/yaml configuration file.
  - Use Container Registry for secure, private storage of Docker images. You can push images to your registry and then you can pull images to any node in cloud or private hosting.
  - Create single- and multi-container pods. Each pod represents a logical host that can contain one or more containers. Containers in a pod work together by sharing resources, such as networking resources. Together, a set of pods might comprise an entire application, a microservice, or one layer in a multi-tier application.
  - Create and manage replication controllers, which manage the creation and deletion of pod replicas based on a template. Replication controllers help to ensure that your application has the resources it needs to run reliably and scale appropriately.
  - Create and manage services. Services create an abstraction layer that decouples frontend clients from pods that provide backend functions. In this way, clients can work without concerns about which pods are being created and deleted at any given moment.
  - Create an external network load balancer.
