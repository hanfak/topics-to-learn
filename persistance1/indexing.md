# Indexing

## What

- problem
  - Imagine a database table with 100 million rows.  This table is used mainly to look up one or two values in each record. To retrieve the values for a specific row you would need to iterate over the table. If it's the very last record that would take a long time!
- Solution
  - Indexing is a way of short cutting to the record that has matching values more efficiently than going through each row.
    - Indexes are typically a data structure that is added to the database that is designed to facilitate fast searching of the database for those specific attributes (fields).
- Example
  - So if the census bureau has 120 million records with names and ages, and you most often need to retrieve lists of people belonging to an age group, then you would index that database on the age attribute.
- Indexing is core to relational databases and is also widely offered on non-relational databases.

## Advantages

## Drawbacks

- When writing a lot, as have to write to index as well
- Data deletion, if not thought about then when deleting data need to delete it in index (which can be tricky)
  - Use of partitioning and partition referencing as a solution
