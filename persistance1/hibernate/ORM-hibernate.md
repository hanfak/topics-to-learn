# ORM - object relational mappers

A pattern that allows the use of a mapper to convert between code (ie java) to database language(ie sql)

## Disadvantages of using orms

- Close coupling of data and business layer
- Lack of control in how ORM implements SQL
- https://completedeveloperpodcast.com/episode-38/
- https://completedeveloperpodcast.com/episode-111/
- https://wozniak.ca/blog/2014/08/03/1/index.html?utm_source=tuicool&amp%3Butm_medium=referral
- 

### Links

- https://blog.oio.de/2016/05/12/orm-vs-sql-when-should-i-use-a-sql-centric-persistence-layer/
- https://www.yegor256.com/2014/12/01/orm-offensive-anti-pattern.html

## Benefits 

### Links 

- https://dev.to/kirekov/junit-5-link-tests-with-task-tracker-issues-2fif

## Links

- https://en.wikipedia.org/wiki/Object-relational_mapping
- https://medium.com/@krzychukosobudzki/repository-design-pattern-bc490b256006
- http://blog.sapiensworks.com/post/2014/06/02/The-Repository-Pattern-For-Dummies.aspx

# Hibernate

A popular ORM for java.

- https://thoughts-on-java.org/hibernate-getting-started/

## Object mapping 

- https://thorben-janssen.com/object-mapper-dto/
  - Using entities which is linked to ORM (JPA/hibernate) and mapping to a DTO which is independent 
  - There are libraries that does this
  - Entities have overheader, while DTO dont 
  - DTO are better for separating concerns between business logic and database impl
  - mapping libraries cause DTO to have downsides of entities