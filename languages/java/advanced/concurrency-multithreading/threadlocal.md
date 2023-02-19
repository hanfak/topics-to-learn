# Threadlocal

- https://howtodoinjava.com/java/multi-threading/when-and-how-to-use-thread-local-variables/
- http://tutorials.jenkov.com/java-concurrency/threadlocal.html
- https://www.baeldung.com/java-threadlocal
- https://www.developer.com/java/java-threadlocal/


## Usage

In a jetty server, we want all request to have access to a constant which is created at the start of request flow (Tracey ID) which is used in all logging in the flow and req to third party apps (Via headers). This Tracey ID is used in monitoring, to help gather all the logs for a particular request to investigate and debug.
