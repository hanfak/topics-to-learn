# Monitoring & Metrics

## Logging

- Types
  - Access
  - Audit
  - Application
- Status
  - ok
  - warn
  - error
- Getting logs to match with same flow/input
- splunk
  - queries
- Passing tracey id from incoming request throughout its entire journey in the app to the outgoing response

## Status pages

- check dependencies are up and running (ie 3rd party api/databases)
  - database up and running and can connect to it
  - 3rd party apis are available and can connect ie return a 200 response
  - Version of the app
  - Specific checks for app is failing
- Check no errors
- Format is correct
  - ie name, description, status
    - description = error message or endpoint api address
    - status = ok , warn , error
  - For aggregators
- Use Concurrency to run all status probes at same time when status probe endpoint is hit.
  - Use caching so that if service is down, can use cached response
- Nagios
  - Checks status page, and send alerts when failing

## Ready pages

- app is up and running
  - can hit the endpoint and get 200
- USed for when depolying app, to check it is up
  - need a smoke test, to run some flow through the app, preferebly with affecting services (ie leaving files to be consumed by 3rd parties, using 3rd party which can block later call, filling up database with useless data)


## Alerting

- When logs error, send an alert
- levels of alert

## Metrics

- Database Metrics
- kubernetes Metrics
- JVM metrics
- Prometheus
- Prometheus alerts
  - getting metrics and setting conditions to alert
- grafana
  - displaying metrics in graphs and tables
