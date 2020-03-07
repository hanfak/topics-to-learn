# Remote Method Invocation

- https://www.quora.com/What-is-RPC-and-RMI

## Cons

- The biggest restriction of this technology was that Java RMI could only be run on a Java Virtual Machine. This meant that the calling application also has to be run on the Java framework in order to make use of Java RMI.
- All of the RPC techniques have one big limitation, and it is that they don't work by the HTTP protocol. Since all applications on the web had to work on this protocol, this used to be a major roadblock for clients which had to access these RPC-style web services.
  - separate ports had to be open for them for clients to access the functionality from these web services.


## Links

- https://docs.oracle.com/javase/8/docs/technotes/guides/rmi/index.html
