# Status pages

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
