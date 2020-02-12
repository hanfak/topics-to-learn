# Relational Database

- types
  - Microsoft SQL Server
  - Oracle
  - MySQL / MariaDB
  - PostgreSQL
  - Microsoft Azure SQL

## What ?

- Relational databases are structured. You have tables and these tables may have dependencies on each other, or relationships.
  -  A database for a store will have a table for customers and one for orders. These two tables are related, because an order is made by a customer.
- A relational database uses SQL which is short for Structured Query Language.
  - This is a fairly rigid and standard way of storing data using tables, columns and rows.
  - Columns represent the data point to be stored
  - A row represents a record with data points per column that has been defined.
  - These are defined in a table which is usually atomic in nature; this means that a table should really only store data records on one entity or object at a time.
    - Eg. A Table Customers should ONLY be storing customer records.
  - When additional details are required, or data needs to be associated with a record from one table to another, then we have what we call relationships.
    - A common key is established between the two (or more) tables and this is used for that association there after.

## When?

- You will enforce the ACID (Atomicity, Consistency, Isolation, Durability) principles.
  - This reduces anomalies, enforces integrity and that is why this is preferred for commerce and financial applications.
- Your data structure is not changing. If you application design is solid and not expected to be changing with future requirements (at least not very often) then you may proceed to use this type of construct and be confident in your data.
-  complex/dynamic queries/reporting are best served from an RDBMS.
- Very mature and support

## Not to use

- your data is structured as a hierarchy or a graph (network) of arbitrary depth,
- the typical access pattern emphasizes reading over writing, or
- there’s no requirement for ad-hoc queries
  - you simply don’t need a relational database with its full-blown query language if there are no unexpected queries anticipated.
  - Dont even need a db, can use a file

## Issues

- Relational databases add a lot of overhead for simple read access. Transactional and referential integrity are powerful, but overkill for some applications.
- RDBMS tables have well-defined and strict schema, so they may not be very easy to alter if a requirement to do so will arise.
- the performance of RDBMS software only noticeably degrades when you start having tables several gigabytes in size.
  - The data is retrieved slowly from large tables because selection queries do table scans and, as the data grows, greater chunks of disk space need to be scanned.
  - This problem can be mitigated by adding indexes, so a much smaller collection of data is scanned before the right data is retrieved.
    - However, indexes have their own problem. Every time new data is inserted, index needs to be updated. This will make insertion operations slow, which may not be so good for multi-user interactivity scenario.
