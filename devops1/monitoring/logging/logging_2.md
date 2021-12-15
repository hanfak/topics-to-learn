# Logging

- Logging is everywhere
- Helps maintain, and keep our programs up and running.
- loggers rot at an unbelievable speed
  - After a while, we find ourselves fixing problems caused by loggers more often than the loggers give us useful information.
  - Code bloat
  - Memory bloat
  - Hard to find messages
  - Hard to link log messages

## What

- Logging is the process of recording application actions and state to a secondary interface.
- loggers don't belong to any particular layers of our systems.
  - Instead, we consider them to be application-wide and shared amongst different components.
  - cross cutting
- logging itself is a subsystem within our application

## Issues

- devs tend to focus on the format rather than the actual purpose of why we are writing logs.


## Rules

- Don’t log
  - Overlogging is detrimental, too much noise to be helpful
  - Logging means more code to maintain, it incurs expense in terms of system performance, and more logging subjects us to more data privacy regulatory audits.
  - https://sobolevn.me/2020/03/do-not-log
  - https://blog.codinghorror.com/the-problem-with-logging/
  - start without logging and work our way up to identify places where we need to log, rather than “log everywhere as we might need to look at them”.
  - rule of thumb for adding a line of logging is “if we can’t pin down an exact reason or a scenario when we will look at the log, don’t log".
- Should be documented using tests

## Scenarios

- catastrophic or unexpected scenarios that requires immediate action (like catastrophic errors that need an application restart)
  - Best to use alerting tools
  - logs give more context around what happened and  possible cause
  - Just like the errors that they accompany, these logs should be kept to a minimum in our code and placed in a single location. They should also be designed/documented in the spec as a required system behavior for error handling. Also, they should be woven into the source code around where the error handling happens.
  - using log.error or log.fatal before a graceful shutdown and restart of the application.
    - attach the full error stack trace and the function or requests’ input data for reproduction if necessary.
- addresses expected, handled errors like network issues and user input validation
  - only requires developers’ attention if there’s an anomaly with them.
  - Together with a monitor set up to alert developers upon an error, these logs are handy to mitigate potential serious infrastructure or security problems
  -  making “visible” for developers, log.warn or log.error can be used
-  Log that should appear most often in our source code – but it's often the most difficult to get right
  -  those associated with the “happy” steps of our applications, indicating the success of operations.
  -  often abused by developers
  -  indicating starting/successful execution operations in our system
    -  interacttions with other apps (req/resp)
    -  who accesses the app
  -  log.info
  -  need to pass the litmus test: are there any circumstances under which we would look at the log (be it a customer support request, an external auditor’s inquiry)?

## Cleaning up logs

-  first step is to identify where the criminals are hiding
  -  A document (or spreadsheet if you would like to be organised)
-  weed out the bad apples
  -  Logs which are duplicated or unreachable are low hanging fruits that we can immediately eliminate from our source code.
  -  others should involve stakeholders
-  urning them into technical requirements with documented purpose for each one of them is essential to nail down a contract
  -  Ask yourself what to do when a log.error happens, and who are we log.info-ing for?
  -
