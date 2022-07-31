# IDs

- These are unique values, primarily used as a way to distinguish different data (even if data in a row is the same)
- This is used for primary keys, indexes etc
- Issues crop up when creating Ids when
  - a lot of unique ids per time interval ie 10000 per second
    - due to lots of writes to the systems
  - Uniqueness constraints may not be possible through default database implementation
  - Type of ids may be constrained due to disk space
    - ie can only have 64 bit, where as a common standard might be UUID (128bit)
  - Ids may be constrained by ordering
    - ie may need to be ordered by date of creation
    - Issues with using time in distributed creation can be clock synchonisation
  - Issues with distributed systems creating ids
    - synchonization problems, may end up with incorrect same id
    - availability of the system 
  - Size of id can limit total number of ids that can Generated
    - Thus need to do a reset or implement a new type of generation and thus migration of old ids

## Creation

### Default database

### Ticket server

### mulit master replication

### UUID

### Twitter snowflake
