

- Get story
- research by devs
- kickoff
- Figure out requirements
- Create branch or work on trunk
- Write acceptance tests which is documented (exposed via html)
  - BDD language
  - Can be whole system up or the part of the system (class or set of classes) which deals with the business logic
    - For whole systems, can track other things (system calls - request sent, database filled, logs written etc)
  - Set up the system for specific requirement - given
    - stuff in database
    - What will third party responses be
    - clocks
    - files
  - Send the input to the system
    - ie a request that will be handled
    - ie an object to a class
  - Assert on visible things that has occured during and after the processing of the request. Only focused on the important parts
    - The response sent be system
    - The return value from method
    - Objects being verified
    - The database/files being filled or updated, at the end or during the process
    - The requests being sent to  external providers
    - performance metrics
- Write code
- tdd, Write unit tests, if not covered by acceptance tests
  - depends on how this is thought about, module design etc
- Decide on documentation tests
- reiterate until all requirements are done
- Refactor
  - to get test passing
  - if code smells are seen
  - when solution to tests is not great
  - as part tdd
- Get feedback from stakeholders
  - can see exposed tests
  - can setup locally, and have demos
- sign off
- QA tests
  - devs will fix any issues which are brough up