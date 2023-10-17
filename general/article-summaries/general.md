# General notes

- Design code as if it will break or do something wrong 
  - In order to fix (curative measure) code should be 
    - highly organised, easy to find what you are looking for
      - modular, loosely coupled, areas isolated, limited number of changes
    - readable
    - use of logging
    - change/fix is easy to make
    - Can rollback
  - In order to prevent, code should be 
    - tested
    - do the minimum
    - least surprise
    - prevent errors entering the system
    - checks by others (pairing/reviews/static analysis) or tested
    - status pages, alerting, liveness probes
    - if somethign goes wrong and can fix automatically (automated Retries or rollbacks)
    - If goes wrongs
      - fail quickly
      - prevent further cascading issues (bulkhead, circuit breakers)