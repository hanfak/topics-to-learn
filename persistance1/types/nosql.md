# NoSQL Databases

- Also know as
  - Document stores
  - Non relational databases
  - schemaless
- Examples
  - MongoDB
  - DynamoDB

## What ?

- Non-relational databases are document-oriented. This so called document type storage allows multiple 'categories' of data to be stored in one construct or Document.
  - A Customer document, would have the customer's information, a sub-category for all their orders, etc.
- Concerns
  - Data structure is highly based around how it will be retrieved and structured based on how it will be read.
  - While relationships between documents are supported to varying degrees,they aren’t treated with the importance that they are in a relational model.
  - The data that is generally read together is generally stored together.
  -  Duplicate data is less of a concern than it would be in a relational model.
- NoSQL databases are document-oriented. Instead of using tables, these documents allow us to store unstructured data in a single document. So a document could contain a customer's details, as well as all their orders to date, their favourites, etc.
- This is more intuitive and requires fewer hops across tables to find all the data relating to a customer.
  - Note however that this results in a need for additional processing effort and more storage as the document sizes grow.
  - The storage will not be as highly organized at with an Relational Database.
- has a less rigid, or, put another way, a more flexible structure to its data
- The data typically is presented as "key-value" pairs.
- NoSQL database properties are sometimes referred to as BASE:


## When ?

- no-sql databases allow far more flexibility and adaptability as you design your application.
- If your data requirements aren’t clear at the outset or if you’re dealing with massive amounts of unstructured data, you may not have the luxury of developing a relational database with clearly defined tables and relationships.
- You are doing Rapid Application Development. No-SQL database supporting rapidly changing designs and coding sprints and is perfect for more Agile settings, where requirements change often.
- You're storing large amounts of data with little to no structure. if your data requirements are not clear, but you know that you need to store lots of data somewhere and somehow, then you can use this database type, which you can morph on the fly to match the requirement.
- To boost horizontal scalability.
  - The CAP (consistency, availability, and partition tolerance) theorem states that in any distributed system, only two of the three CAP properties can be used simultaneously. Adjusting these properties in favor of strong partition tolerance enables NoSQL users to boost horizontal scalability.
- NoSQL typically favours a denormalised schema due to no support for JOINs per the RDBMS world. So you would usually have a flattened, denormalized representation of your data.
- Read/Write throughput is very high
- Will support Bigdata in volumes of Terra Bytes & Peta Bytes
- Can be hosted in cheaper hardware machines
- In memory caching option is available to increase the performance of queries
- were specifically designed for high availability and performance
- at their core, these databases hold data in a hash-table-like structure, they are extremely fast, simple and easy to use, and are perfect for use cases like
  - caching,
  - environment variables,
  - configuration files
  - session state etc.
- https://www.networkworld.com/article/2999856/10-use-cases-where-nosql-will-outperform-sql.html
- http://highscalability.com/blog/2010/12/6/what-the-heck-are-you-actually-using-nosql-for.html

## Types

- This flexibility makes them perfect for using in memory (e.g. Memcached) and also in persistent storage (e.g. DynamoDb).
- There are other "JSON-like" databases called document databases like the well-loved MongoDb, and at the core these are also "key-value" stores.

## ISsues

- NoSQL DBs often lack the ability to perform atomic operations across multiple "tables".
-  Most of NoSQL systems employ eventual consistency, which means that, after update happens, it will take some time for related data and database replicas to be updated. Data sometimes is lost in his process. Not good if you need to keep your records precise.
