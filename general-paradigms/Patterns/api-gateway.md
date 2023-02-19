# Api gateway

- An API gateway is a server that acts as a single point of entry for a set of microservices.

## Usages

- Routing
- Authentication and Authorization
  - authenticate clients and enforce access control policies for the microservices
- Rate limiting
- Load balancing
- Caching
- Monitoring
  - collect metrics and other data about requests and responses
- Transformation
  - transform the data received from the microservices into a format that is more convenient for the clients or servers to use
  - To different formats, or aggregating data for clietns
  - Request and response validation
- Service discovery
  - discover the available microservices and their locations, enabling the clients to access them without knowing their specific addresses
- Circuit breaker
  -  prevent a single failed microservice from bringing down the entire system. The circuit breaker can monitor the health of the microservices and automatically fail over to a backup service if necessary.

## Advantages

- Improved performance
  - enabling it to handle a larger number of requests and respond more quickly to the clients.
- Simplified system design
  - makes it easier for the clients to access the various microservices.
- Enhanced security
- Improved scalability
  - By load balancing
- Better monitoring and visibility

## Disadvantages
- Increased complexity
  - increase managing and maintainability
- Performance overhead
  - another request
- Single point of failure
  - Can be mitagated by using a hot standby

- https://levelup.gitconnected.com/system-design-interview-basics-difference-between-api-gateway-and-load-balancer-60260b568121
- https://medium.com/geekculture/system-design-basics-what-is-an-api-gateway-b858e9491608
