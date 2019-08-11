# Entry point

How to communicate with a program.

- Http
    - Using a client via some other application (service or web based)
    - Pass information via query params or standard format (json/xml)
  - REST
  - SOAP
- Scheduled Jobs
  - Jobs that run on a timer (ie cron/quartz) and access some part of your application (either internal or via http by a client)
- GUI
  - local ie mobile or desktop app
  - Browser based via web page (html/js)
- Command line
- Hessian or serialized objects - pass objects between each other
- Database/files changes - any changes in anything that it is watching or using it will pick up and process
