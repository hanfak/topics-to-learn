# Proxy

## What

- allows us to create an intermediary that acts as an interface to another resource, while hiding the underlying complexity of the component
- Example
  - Consider a heavy Java object (like a JDBC connection or a SessionFactory) that requires some initial configuration.
  - We only want such objects to be initialized on demand, and once they are, we'd want to reuse them for all calls
- Example
  - When we download multiple of the same file, can cache it after first download and reuse it
- Provide a surrogate or placeholder for another object to control access to it.
- Use an extra level of indirection to support distributed, controlled, or intelligent access.
- Add a wrapper and delegation to protect the real component from undue complexity.
- Controls and manage access to the object they are protecting
- AKA surrogate, handles and wrappers.
- instantiates the real object the first time the client makes a request of the proxy, remembers the identity of this real object, and forwards the instigating request to this real object.
  - Then all subsequent requests are simply forwarded directly to the encapsulated real object
- proxies can be chained together

## When to reuse

- Virtual Proxy
  - When we want a simplified version of a complex or heavy object.
  - In this case, we may represent it with a skeleton object which loads the original object on demand, also called as lazy initialization.
  - These proxies will provide some default and instant results if the real object is supposed to take some time to produce results. These proxies initiate the operation on real objects and provide a default result to the application. Once the real object is done, these proxies push the actual data to the client where it has provided dummy data earlier.
  - links
    - https://www.educative.io/answers/what-is-the-virtual-proxy-design-pattern
- Remote Proxy
  - When the original object is present in different address space, and we want to represent it locally.
  - We can create a proxy which does all the necessary boilerplate stuff like creating and maintaining the connection, encoding, decoding, etc., while the client accesses it as it was present in their local address space.
  - This is what the "stub" code in RPC and CORBA provides
  - Talking to the real object might involve marshalling and unmarshalling of data and talking to the remote object. All that logic is encapsulated in these proxies and the client application need not worry about them.
- Protection Proxy
  - When we want to add a layer of security to the original underlying object to provide controlled access based on access rights of the client.
- A smart proxy
  - interposes additional actions when an object is accessed.
  - Counting the number of references to the real object so that it can be freed automatically when there are no more references (aka smart pointer),
  - Loading a persistent object into memory when it's first referenced,
  - Checking that the real object is locked before it is accessed to ensure that no other object can change it.
- logging proxy
  - when you want to keep a history of requests to the service object.
  - The proxy can log each request before passing it to the service.
- caching proxy
  - Caching request results
  - when you need to cache results of client requests and manage the life cycle of this cache, especially if results are quite large.
  - The proxy can implement caching for recurring requests that always yield the same results. The proxy may use the parameters of requests as the cache keys.
- Smart reference.
  - This is when you need to be able to dismiss a heavyweight object once there are no clients that use it.
  - The proxy can keep track of clients that obtained a reference to the service object or its results. From time to time, the proxy may go over the clients and check whether they are still active. If the client list gets empty, the proxy might dismiss the service object and free the underlying system resources.
  - The proxy can also track whether the client had modified the service object. Then the unchanged objects may be reused by other clients.

## structure

- The Service Interface declares the interface of the Service. The proxy must follow this interface to be able to disguise itself as a service object.
- The Service is a class that provides some useful business logic.
- The Proxy class has a reference field that points to a service object. After the proxy finishes its processing (e.g., lazy initialization, logging, access control, caching, etc.), it passes the request to the service object.
  - Usually, proxies manage the full lifecycle of their service objects.
- The Client should work with both services and proxies via the same interface. This way you can pass a proxy into any code that expects a service object.
-

## Advantages

- security
- avoids duplication of objects which might be huge size and memory intensive. This in turn increases the performance of the application.
- The remote proxy also ensures about security by installing the local code proxy (stub) in the client machine and then accessing the server with help of the remote code.
- You can control the service object without clients knowing about it.
- You can manage the lifecycle of the service object when clients don’t care about it.
- The proxy works even if the service object isn’t ready or is not available.
- You can introduce new proxies without changing the service or clients.

## Drawbacks

- This pattern introduces another layer of abstraction which sometimes may be an issue if the RealSubject code is accessed by some of the clients directly and some of them might access the Proxy classes. This might cause disparate behaviour.
- The response from the service might get delayed.


## Compared to other patterns

- Proxy provides the same interface.
  - Decorator provides an enhanced interface.
  - Adapter provides a different interface to its subject.
- Decorator and Proxy have different purposes but similar structures. Both describe how to provide a level of indirection to another object, and the implementations keep a reference to the object to which they forward requests.
- Facade is similar to Proxy in that both buffer a complex entity and initialize it on its own. Unlike Facade, Proxy has the same interface as its service object, which makes them interchangeable
- Decorator and Proxy have similar structures, but very different intents. Both patterns are built on the composition principle, where one object is supposed to delegate some of the work to another. The difference is that a Proxy usually manages the life cycle of its service object on its own, whereas the composition of Decorators is always controlled by the client.

## Links

- https://www.youtube.com/watch?v=NwaabHqPHeM&index=11&list=PLrhzvIcii6GNjpARdnO4ueTUAVR9eMBpc&t=0s
- https://medium.com/@mithunsasidharan/understanding-the-proxy-design-pattern-5e63fe38052a
- https://www.javacodegeeks.com/2015/09/proxy-design-pattern.html

## Types

- http://www.blackwasp.co.uk/Proxy.aspx
- https://www.oodesign.com/proxy-pattern.html
