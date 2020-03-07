# H2 Db in Spring

- Can use an inmemory database, normally H2
  - Normally not used in production, but useful for tests/local usage

## In Spring

- When starting Spring, we get a line similar to
  ```
  2020-02-24 19:19:02.421  INFO 41396 --- [           main] o.s.b.a.h2.H2ConsoleAutoConfiguration    : H2 console available at '/h2-console'. Database available at 'jdbc:h2:mem:testdb'
  ```
- In the browser, you can access the H2 console, by going to `http://localhost:8080/h2-console`
  - Or what ever port you set in the properties
- To access the database, copy the address, into browser form, and test connection, the connect.
