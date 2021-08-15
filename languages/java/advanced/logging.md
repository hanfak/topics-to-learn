# Logging

See devops/monitoring/logging for more details


## What to log

Majority of what will be logged, will be sad path, or things that should not happen (exceptions). This can be different depending on the business or technical concerns for the app. But need to be careful cause logs can build up (take up space) which leads to searching can be expensive (time and money - splunk licenses)

For example, logging the steps in accessing the database to do access. This is a common task, it will populate the logs quickly. But this can be essential when debugging when an issue in production occurs.

### Common patterns

- Log exceptions, put the stack trace (exception) in the log
- Use right level of logs (Info, debug, warn, error etc)
- Add debug logs, which can be turned on or off when needed, to avoid too many logs in production
- Allow exception to bubble up, and handle them in upstream in the app


### Other areas
- audit request and response
- who accesses app

See devops/monitoring/logging for more details

In java, the use of logging libraries are used to write logs

Popular libraries:

- Slfj
  - A interface which work with many logging libraries
- Logback
  - use of logback xml files for config
- Log4j
- java library

Loggin is crosscutting concern. To deal with this can use:
- AOP
  - Use decorators
    - catch exceptions which log it
  - use tool (spring annotations)
- inject loggers into classes
  - breaks SRP

## Testing logs

- Some dont believe in this
- Helps maintain correct log output messages when changes occurs
- Methods
  - Use a stub which implements slf4j interface and inject in
  - Can grab the output (system.out) point to your own and check they contain correct logs
    - good for integration or end to end tests


## Links

- https://www.baeldung.com/spring-boot-logging
