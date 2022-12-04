# Connection pooling

- A pattern used with storing already precreated connections to a db, which can be used when talking to a database instead of connecting anew to a database.
- Similar to the pattern of object pooling


## Benefits
- speed, faster to use already created connections rather than alway creating new connections

## Libraries

- Java
  - HikariCP
  - C3po

## Improving

- More threads only perform better when blocking creates opportunities for executing.
  - As blocking because of waiting for IO to execute (thus more threads is better for old HDD rather than SSD)
- More threads than CPUs means context switching, due to time slicing, is slower than one thread per cpu
- You want a small pool, saturated with threads waiting for connections.

- https://github.com/brettwooldridge/HikariCP/wiki/About-Pool-Sizing
