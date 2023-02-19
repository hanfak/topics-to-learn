# Sidecars

- Instead of using libraries within the app to handle communications we use a proxy to do most of the work
- Instead of using a complex protocol, which needs a complex library, can more this complexity to a proxy and communicate to it via a simple protocol within a simple client

## How

- Each client has a sidecar proxy
- The client will redirect all requests to the sidecar
- The side car will change how it communicates (ie add headers, use tls) and communicate with other sidecar in front of the app you wish to talk to
-  the recieving side car will then translate to another protocol that is compatible with the receiver app
- Generally, the side car is attached to the app. So if the app goes done the side car goes down
  - not necessary
- Service mesh is based on this  ie istio
- Must be layer 7 proxy

## Benefits

- Decoupling how you communicate
  - If want to use a different protocol, the app does not need to change only the side car
- protocol upgrade easily
- language agnostic
  - using library means you are tied to using a library in the language
- Easy to use security
  - can hook up to somethign like vault, and certificates are handled automatically 
- Tracing and monitoring
  - easy to follow requests in service mesh
- service discovery
  - use of internal dns system
  - so if a new service and side car is created, the service mesh will add it to he dns system, and make it easy for other services to pick it up and talk to the new service
- Can do caching
## Issues

- Extra hops in communications - latency
  - which leads to more chance of failure
- The communication between the side car can be very heavy
- side car needs to be monitoried
- extra complexity
