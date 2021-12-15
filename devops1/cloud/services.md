# Cloud Services

## Types of Services

- Computing and hosting
- Storage
- Databases
- Networking
- Big data
- Machine learning

## Computing and hosting services

- Types
  - Work in a serverless environment. FaaS
  - Use a managed application platform. PaaS
  - Leverage container technologies to gain lots of flexibility. CaaS
  - Build your own cloud-based infrastructure
- Each type uses a combination of services/resources provided by the cloud provider to optimise these types

## Storage Services

- Whatever your application, you'll probably need to store some media files (streaming videos ), backups, or other file-like objects.
- These services are provided depending on how many times it is accessed
- Fully managed NFS file servers
  - For transfering files

## Database Services

- Providing access to a host of databases that your app will use
- Normally a provider will have their own custom built database
  - but you can attach a third party cloud database that you use or easy to migrate to

## Network Services

- These services help you to load-balance traffic across resources, create DNS records, and connect your existing network to cloud's network.
- Features
  - Virtual Private Cloud (VPC) provides a set of networking services that your VM instances use. An instance can have more than one interface, but each interface must be connected to a different network. Every VPC project has a default network.
  - Firewall govern traffic coming into instances on a network. The default network has a default set of firewall rules, and you can create custom rules
  - Routing lets you implement more advanced networking functions in your instances, such as creating VPNs. Routing specifies how packets leaving an instance should be directed. For example, a route might specify that packets destined for a particular network range should be handled by a gateway virtual machine instance that you configure and operate.
  - Load balancer
    - to distribute the workload across multiple instances
    - Network load balancing lets you distribute traffic among server instances in the same region based on incoming IP protocol data, such as address, port, and protocol. Network load balancing is a great solution if, for example, you want to meet the demands of increasing traffic to your website.
    - HTTP(S) load balancing enables you to distribute traffic across regions so you can ensure that requests are routed to the closest region or, in the event of a failure or over-capacity limitations, to a healthy instance in the next closest region.
      - You can also use HTTP(S) load balancing to distribute traffic based on content type. For example, you might set up your servers to deliver static content, such as images and CSS, from one server and dynamic content, such as PHP pages, from a different server. The load balancer can direct each request to the server that provides each content type.
  - You can publish and maintain Domain Name System (DNS) records

  ## Big Data Services

  - Asynchronous messaging
    -

  ## Machine Learning Services
