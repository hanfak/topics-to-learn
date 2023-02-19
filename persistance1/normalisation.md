# Normalisation

## what

- technique of organizing the data in the database

### 1NF

should follow the following 4 rules:

1. It should only have single(atomic) valued attributes/columns.
2. Values stored in a column should be of the same domain
3. All the columns in a table should have unique names.
4. the order in which data is stored, does not matter.

- requiring no repeating elements or groups of elements. Remove duplicate columns from the same table. Create separate tables for each group of related data. Identify each set of related data with a primary key.
### 2NF

Should follow:

- It should be in the First Normal form.
- it should not have Partial Dependency.

### 3NF
Should follow:
- It is in the Second Normal form.
- it doesn't have Transitive Dependency.

#### Boyce and Codd Normal Form

### 4NF

- It is in the Boyce-Codd Normal Form.
- it doesn't have Multi-Valued Dependency.
### 5NF


## Why

- To reduce the need for restructuring the collection of relations, as new types of data are introduced, and thus increase the life span of application programs.
- Updates run quickly due to no data being duplicated in multiple locations.
- Inserts run quickly since there is only a single insertion point for a piece of data and no duplication is required.
- When deleting data you may have to remove more than intended. Removing some information requires removing unrelated information
- Tables are typically smaller than the tables found in non-normalized databases. This usually allows the tables to fit into the buffer, thus offering faster performance.
- Data integrity and consistency is an absolute must if the database must be ACID compliant. A normalized database helps immensely with such an undertaking.
- Flattened tables(Denormalised) may not allow for partial information to be inserted. This may result in being unable to store some information.
- excessive disk I/O
- extensive data redundancy
- Saves space
  - But space is cheap
- Prevent
  - Insertion Anomaly
  - Updation Anomaly
  - Deletion Anomaly

## Issues
- Since data is not duplicated, table joins are required
  - makes queries more complicated, and thus read times are slower.
- Since joins are required, indexing does not work as efficiently
  - this makes read times slower because the joins don't typically work well with indexing.
- Normalized design is difficult.
- Due to spread out nature of data, queries can become complex
- Should not be done for non relational databases
- Simplifies updates, but this makes reads complex
  - But most databases are used for reads, so should design for that

## when

## Links

- https://www.studytonight.com/dbms/database-normalization.php
- https://youtu.be/GFQaEYEc8_8
- https://completedeveloperpodcast.com/episode-135/
- https://www.lifewire.com/database-normalization-basics-1019735
- http://phlonx.com/resources/nf3/
- https://www.essentialsql.com/database-normalization/
