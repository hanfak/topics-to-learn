# Java Persistence API (JPA)

## What

- An API specification (ie hibernate is written to)
- https://en.wikipedia.org/wiki/Java_Persistence_API
- A persistence entity is a lightweight Java class whose state is typically persisted to a table in a relational database
- Use of POJOs as entities
  - The pojos will need a zero arg constructor to work
  - It will need an id, which is for the jpa to interact with the database
- Handles all the JDBC and sql implementations

## Advantages

- https://www.sitepoint.com/5-reasons-to-use-jpa-hibernate/

## Negatives

- Add one more thing you have to worry about (if you have a complex database interactions).
- JPA Have limitations, that is the reason for have a Native interface, you can send Native SQL sentences to database soooooo, you can survive without JPA or any ORM.
- It’s heavyweight, it creates a complete environment that you almost never need.
- Forces domain objects to hold database specific knowledge

## Linkage

- Need to override Equals and Hashcode, due to id field in entity
  - We will use the id to determine the object equality

## Mappings

- Linking entity pojos, with each other in code which will be mimicd in the database ie parent child many to many
