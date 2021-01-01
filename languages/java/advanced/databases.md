# Database and java

- Be wary of using ORMs and use the simplest tool (which might be using plain sql)
- Sql is a declarative language, and is not hard to learn. Very useful for working with relational databases
- Dont be too quick to go straight to modelling tables as objects and using ORMs, when calling a sql is a simpler
  - Using ORMs means a lot set up and code (more code, more chance of bugs), learning a DSL, testing, relying on the ORM to generate non efficient queries,
- Benefits of using Sql
  - We don’t need a new table for the join output, so we don’t create one.
    - The biggest failing of applied object-oriented programming has been the belief that you should faithfully reproduce your domain model in code.
    - In reality, a few core type definitions are useful for encapsulation and understanding, but tuples, sets, arrays, and so forth are all we need the rest of the time.
    - Unnecessary classes become a burden as the code evolves.
  - The query is declarative
    - Nowhere does it tell the database how to do the query; it just states the relational constraints the database must satisfy
    - Doing this in java (exp pre version 8), it would be done imperatively
    - Instead, we should declare constraints and desired outcomes, and then isolate the how implementation in one place or delegate to a library that can implement it for us
  - The database is more efficient at running the query then letting the code run query on the whole dataset
  - The domain-specific language (DSL) is well matched to the problem
    - SQL is mature, and well known, with lots of resources
