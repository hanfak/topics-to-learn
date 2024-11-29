# Java Persistence API (JPA)

## What

- An API specification (ie hibernate is written to)
- https://en.wikipedia.org/wiki/Java_Persistence_API
- A persistence entity is a lightweight Java class whose state is typically persisted to a table in a relational database
- Use of POJOs as entities
  - The pojos will need a zero arg constructor to work
  - It will need an id, which is for the jpa to interact with the database
- Handles all the JDBC and sql implementations
- https://vladmihalcea.com/best-spring-data-jparepository/

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

## Patterns

- https://vladmihalcea.com/spring-data-findall-anti-pattern/
  -  you should not really offer your clients a way to fetch an entire database table
  - define a new base interface by extending the Repository interface instead of the JpaRepository and declaring explicitly which methods are allowed to be inherited by your custom repositories
  ```java
  public interface BaseJpaRepository<T, ID> extends Repository<T, ID> {
 
    Optional<T> findById(ID id);
 
    T getReferenceById(ID id);
     
    boolean existsById(ID id);
     
    void deleteById(ID id);
 
    void delete(T entity);
     
    long count(); 
  } 
  ```
  -   the entities that have a large number of records can now define their specific Repository interface by extending the BaseJpaRepository
  - the entities with a small number of records can extend the default Spring Data JpaRepository

## Links 

- https://www.youtube.com/watch?v=mcl_nibV39s  The ULTIMATE Guide for Spring Data JPA & Hibernate | 5 Hours Tutorial 
- https://www.youtube.com/watch?v=exqfB1WaqIw  Performance oriented Spring Data JPA & Hibernate by Maciej Walkowiak 
  - https://github.com/Kehrlann/spring-security-the-good-parts
- https://www.youtube.com/watch?v=iJ2muJniikY  Spring Security, demystified by Daniel Garnier Moiroux
  - 