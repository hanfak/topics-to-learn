## TraceyID

### Links

- http://opentracing.io/documentation/

## Servlets

- Filters
  - logging incoming requests and outgoing responses via filter
- Servlet
  - extends HttpServlet
  - gets the request and sends the response
    - you deal with the request and form the response


### Links

- https://en.wikipedia.org/wiki/Java_servlet
- https://stackoverflow.com/questions/7213541/what-is-java-servlet
- http://www.baeldung.com/intro-to-servlets
- http://tutorials.jenkov.com/java-servlets/index.html

## Jetty

- Server
  - stop and start web server, to accept requests
  - setup with a handler containing the servlets and filters
- ContextHandler
  - adds the servlets to the handler
- setHandler
  - Passing the handler
- addFilter
  - add filter to handler
