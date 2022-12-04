# Logging

- https://www.marcobehler.com/guides/java-logging
## What

- Logging is the process of recording application actions and state to a secondary interface.
-  Loggers don't belong to any layers of our systems. Instead, we consider them to be application-wide and shared amongst different components.
  - It is a cross cutting concern
### Analogy - medicine
- Similar to medicine, have two parts prevention and cure
- Prevention is like vaccine, lifestyle etc
  - You stop the issue from happening, or stop it getting worse
- Cure, is like drugs after finding out you are ill  
  - logs are like this, they will inform you that something is wrong, help you find the issue (if they are implemented correctly) and allow us to fix it (ie code change, data fix, manual fix etc)

## users

- The people that will use it
- These can be:
  - The Devs
  - tech ops
  - business

## Why

- To help with monitoring the application when it is live
- To find out where the problem occured, when it occured, what happenend (stack trace)
  - Will help tech support to solve problems out side of code (via app, database, calls to third party)
  - Starting point to solve problems and debug within code, with the aim of immitating the issue locally
- If metrics involved, ie number of calls by same ip, or response time is long, these can be hooked up to some alerting system and if break threshold will alert
  - But generally should be done using metrics like prometheus
- A requirement by techops/monitoring team and no way around this
- A requirement by regulation
  - although can use database, and export as views to a datawarehouse

## When

- Dependent on needs of business and monitoring
- Generally look at logs to reveal
  - what went wrong
  - if something went wrong multiple times above some threshold
  - If some secruity issue popped up
  - View the whole flow, including calls to db/services
- Should look at logging sad paths, exceptions,
- If possible somethings dont need to be logged, but gained from metrics produced by app or from external tooling monitoring app
  - but not always possible, so may need to add logging for this
    - ie time a request to took
- Might be possible to grab some logs by placing a proxy/sidecar in front of app that monitors/intercepts calls to the app
  - this can be help help to get timings of call, payloads in and out, who called it (if using an ingress in kubernetes can use logs there)
- Not everything should be logged,
  - to much and can lead to too much to search (long running queries),
  - too much noise
  - Hard disk used up, application searching slows down
  - Too much noise in code base
  - Repetitive noise (as majority calls will be happy path)
  -

## Testing during development

- Differing views on this
- The log is part of code, and should be covered by tests, esp if doing TDD.
  - Again views are different on whether the message should be tested or happy to verify that a log was called
- Generally it is hard to test logs as unit test, better to do this manually
  - This happens if using annotation or newing the logger in the class as a field (using some logger factory)
  - To avoid this can inject a logger in the constructor, then use a logger stub which acts as map  or mock (ie mockito) to make it easier to test
    - but increase dependencies
- Can test in and end to end way by capturing standard output to someobject or file, or if logs are put into files as part of app process
- Can test manually, bu looking at the log file or app output

## How

- logging libraries used in code
  - Using logger factory
    - constructor injection
    - field instantiation
- When exceptions are caught, includes stack trace
- When exceptions are not caught during flow, but captured by the top layer (ie some sort of error handler)
- Tracey id
  - which populates all requests and logs within that current flow upto and including the outgoing response
  - Use of Threadlocal, as a cache to populate a UUID, and get it whenever we need the tracey id


## Types

- Application Logs
- Access Logs
- Audit Logs

## Logging Levels

## Capturing

- Stored to an output files, backed up, normally saved for x days before deletion, can lead to lots of hard disk usage
- Standard output, using a stream

## Monitoring

- Splunk

## Tooling

- ELK
  - elastisearch
  - Logstash
  - Kibana

## Logback

## SLF4J

## Links

- https://dzone.com/articles/java-logs-4-types-of-logs-you-need-to-know
- https://www.freecodecamp.org/news/how-to-use-logs-effectively-in-your-code/
- https://www.codeproject.com/Articles/42354/The-Art-of-Logging
- https://sobolevn.me/2020/03/do-not-log

- Libraries
  - Logback
    - https://examples.javacodegeeks.com/enterprise-java/logback/logback-custom-appender-example/
  - slf4j
    - https://examples.javacodegeeks.com/enterprise-java/slf4j/slf4j-tutorial-beginners/
- levels
  - info
  - warn
  - error
  - debug
- Format
  - data
  - class
  - line
  - message
  - type
  - level
- Types of logs
  - application
    - include stack trace
  - audit
    - incomnig and outgoing requests and repsonses
      - via filters in servlets
    - internal req and rsp
  - access
    - when app has been accessed
- Appenders
  - layouts
  - Types
    - console
    - files
- Configuration
  - properties files
  - xml
- Link all logs that relate to one request from beginner to outgoing response
  - use tracey id
  - use id
