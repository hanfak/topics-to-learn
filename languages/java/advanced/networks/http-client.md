# HTTP client

## What ??

It allows the user to code a request and execute using http protocol over tcp/ip and hit a http server (which is open to receiving a request and responds). It will get a response from the server, and the code and handle this anyway it likes.

- https://www.quora.com/What-is-the-difference-between-HTTP-client-and-HTTP-server

## Use??

- It is used if program needs to send a request to a third party server (ie some api) and does something with the response.
- In testing a server, via integration test. The app runs a server, and the test need to send a request, to check the request is processed correctly by the server.

NOTE: Using a browser or postman can do this for us, if we want to do manual requests. But we will only get a response and not be able to do anything with this.


## Using libraries

- Common library to use is `https://hc.apache.org/httpcomponents-client-ga/`

## Using socket client


## Links

- https://hc.apache.org/httpcomponents-client-ga/quickstart.html
- https://self-learning-java-tutorial.blogspot.co.uk/2015/10/apache-http-client-tutorial.html
§
