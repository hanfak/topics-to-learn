# Apis and communications between apps

Communications between different applications/businesses as either the human user or another application. Some business functionallity might need to be split into several apps so that they can managed properly, worked on separately, hide implementation, designed better but they will have to all communicate with one another to provide a business service. This means that apps needs to talk to each other and there are a few ways of doing this.

- Http/webservices
  - REST
  - soap
    - Going to one end point, and the body and/or headers determine how it will be processed
  - https://stackoverflow.com/questions/19884295/soap-vs-rest-differences
  - GUI/front end

- JMS
- Hessian

- External source
  - Ftp/sftp
  - database


- desktop gui
  - javafx gui

- Libraries and frameworks
  - called with the application



- Fixed API to communicate with
  - advantages?
  - disadvantages?
    - others rely on it, it cannot change it is fixed. Otherwise other services may break.

- Consumer driven contract testing
- stubbing 3rd party apps for testing

## Push/Pull

- polling/reading
  - making request regularly
  - use of scheduled job ie quartz
- pushing
  - app pushes stuff to your app regularly

- https://simplicable.com/new/pull-vs-push-technology

- Crawlers
  - form of polling
  - cover feeds/webpage for info
- Web sockets
