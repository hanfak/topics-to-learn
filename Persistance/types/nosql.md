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
- NoSQL databases are document-oriented. Instead of using tables, these documents allow us to store unstructured data in a single document. So a document could contain a customer's details, as well as all their orders to date, their favourites, etc.
- This is more intuitive and requires fewer hops across tables to find all the data relating to a customer.
  - Note however that this results in a need for additional processing effort and more storage as the document sizes grow.
  - The storage will not be as highly organized at with an Relational Database.


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

## ISsues

- NoSQL DBs often lack the ability to perform atomic operations across multiple "tables".
-  Most of NoSQL systems employ eventual consistency, which means that, after update happens, it will take some time for related data and database replicas to be updated. Data sometimes is lost in his process. Not good if you need to keep your records precise.
