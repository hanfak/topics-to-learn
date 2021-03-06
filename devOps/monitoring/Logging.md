# logging

- Types
  - Access
    - Who and when accessed the app (ie ip, user id) and what parts of the apps (ie uri paths)
  - Audit
    - Audit logging captures significant events in the system and are what management and the legal eagles are interested in. This is things like who signed off on something, who did what edits, etc.
    - What comes into and out of the system (http request/response)
  - Application/diagnostic
    - Capturing exceptions, processes
- Status
  - info
  - warn
  - error
    - Passing stack trace
  - debug
    - everything possible
    - Should be turned off for prod, and only used for locally or turned on via properties in prod when need to find a problem
- Format
  - timestamp
  - classes
  - message
    - exceptions
    - key terms
    - obfuscated sensitive data
- Getting logs to match with same flow/input
  - use of tracey id
  - Makes it easier to search and have all logs for one flow through system
    - especially when logs of different requests are interspered
- splunk
  - queries
- Passing tracey id from incoming request throughout its entire journey in the app to the outgoing response
- https://www.dynatrace.com/resources/ebooks/javabook/collecting-performance-data/
- Via
  - Stdout
  - files
    - application specific
  - database
- Why?
  -  monitoring, troubleshooting and debugging.
- Secruity
- Avoid using for performance

## Links

- https://completedeveloperpodcast.com/episode-73/
