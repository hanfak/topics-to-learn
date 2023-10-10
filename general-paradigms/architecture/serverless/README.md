# Serverless

## What?

- an approach to software design that allows developers to build and run services without having to manage the underlying infrastructure.
  - Developers can write and deploy code, while a cloud provider provisions servers to run their applications, databases, and storage systems at any scale.
- A service that is only run when it is called
- Gained popularity from AWS lambdas
- Need app that can start up quickly to process a request

## How

## For

- No server management.
  - Serverless computing runs on servers, but those servers are managed by cloud service providers
- Save cost
  - With traditional server architecture, you would have to predict and purchase server capacity, usually more than you need, to ensure your application does not face any performance bottlenecks or downtime
  - With serverless, cloud service providers only charge you for what you use since your code will only run once triggered by an event when a backend service is needed
  - serverless saves a fortune in human resource costs as well. As maintance of servers are already handled in the price
- Scalability.
  - Applications built on serverless architecture can be scaled endlessly and automatically.
- Quicker time to market
  - Development environments are easier to set up and not having to manage servers leads to accelerated delivery and rapid deployment.
- Reduced latency.
  - Thanks to Content Delivery Networks (CDN) and Edge Networks, serverless functions can be run on servers that are closer to end users all over the globe

## Against

- Vendor lock-in
  -  the easiest way to go will be to use a single cloud services provider
  - Each provider will have their own way of doing things, so big changes if want to migrate
  - If there is an infrastructure problem of any kind, you have to wait for them to fix it.
    - Or you will need to have a back up server that turns on to serve traffic (ie kubernetes cluster)
- Security
  - Cloud providers will often run code from several customers on the same server at any given time
   - via Multitenancy. customers are tenants that only have access to their share of the server  
   -  data could be exposed due to misconfiguration of that server.
- Performance impact
  - When a function is called for the first time, it requires a “cold start” which is to say that a container needs to spin up before the function can be run.
    - container will continue to run for a period of time after the API call is complete in case it is needed again soon after at which point we get a “warm start” without the added latency.
    - This can reduce the number of technologies that you can use in serverless due to SLA requirements or make this a non option due to a non negotiable requirement for specific tech
- Debugging and testing.
    - a serverless environment can be difficult to replicate in order to perform integration tests. 
### Links
- https://blog.cyborch.com/the-case-against-serverless/

## Links

- https://medium.com/@AlexeyBalchunas/make-any-java-web-app-serverless-786119ffdf83
- https://www.javacodegeeks.com/2019/06/build-first-serverless-function-minutes.html
- https://www.exoscale.com/syslog/java-serverless-micronaut-graalvm/
- https://www.datadoghq.com/knowledge-center/serverless-architecture/
- https://martinfowler.com/articles/serverless.html
- https://www.redhat.com/en/topics/cloud-native-apps/what-is-serverless
