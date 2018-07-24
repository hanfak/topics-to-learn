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

## WARS on containers, external servers, external vs embedded servers

- https://steveperkins.com/war-files-vs-embedded-servers/
- https://www.dynatrace.com/news/blog/the-era-of-servlet-containers-is-over/
- https://stackoverflow.com/questions/12689910/difference-between-web-server-web-container-and-application-server
- https://stackoverflow.com/questions/936197/what-is-the-difference-between-application-server-and-web-server
- https://www.theserverside.com/feature/Understanding-How-the-Application-Servers-Web-Container-Works
- https://www.quora.com/Is-Tomcat-a-web-server-or-a-web-container
- https://techspirited.com/web-container-vs-web-server
- https://stackoverflow.com/questions/23176717/embedded-vs-non-embedded-java-server
- http://stephencoakley.com/2017/07/06/embedded-vs-external-web-server
- https://www.beyondjava.net/blog/application-servers-sort-of-dead
- https://www.reddit.com/r/java/comments/36nt73/war_vs_containerless_spring_boot_etc/?utm_source=amp&utm_medium=comment_list

## Tomcat/catlina

- https://www.mulesoft.com/tcat/tomcat-catalina
