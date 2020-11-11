# Relational Vs Document Databases

## One to one relationships

- In a relational database, you might model such relationships in a single table, or in two tables with a relationship between them.
- In general, in a document database, you would simply put it all in a single document, with nullable fields as required.
  - This is a simple case, but gets rid of a join.
  - Updating either record requires an update of the document.

## One to (not too) many relationships.

- In a relational database, this is going to be expressed as a parent table, with a child table that has a foreign key back to the parent. In the relational model, you’d retrieve the parent and children in one shot by either returning two recordsets, or by using a join to flatten the relationship.
- In a document database, if the children are not relevant without the parents, you’d simply have an array in the document being stored. Retrieval of this dataset would not require a join and would not require parsing, but updating a child record would require you to update the parent document.

## One to (a great) many relationships.

- In a relational database, this would again be expressed as two tables joined with a foreign key (and hopefully with some appropriate indices).
- In a document database, this typically would not all be stored in the manner previously outlined, because any retrieval of the parent brings back all the child records.
  - Instead, you would typically store the child records as their own documents, with a reference back to the parent. That way you could grab sane recordsets without getting humongous amounts of data.
  - This can be interesting as more child records pile up, but you could also use a hybrid approach.

## Many to Many relationships

- In a relational database model, this would be expressed by having two entity tables, with a join table between them. Multiple joins would be used for retrieval.
- This gets interesting in document databases, because the model is no longer based around entities, but around how they are read. It’s entirely possible that you might express such a relationship with two separate documents, one for each end of the relationship. Each would have its related keys stored as an array under the aggregate root. This can be interesting in terms of keeping both documents up to date.

## Hierarchies

- In relational databases, this will either be modeled using some sort of hierarchyid type (and related functions) or simply be a long chain of foreign keys. The latter is extremely annoying,  as you can end up with an unknown number of joins.
- In a document database, you have many options.
  - For instance, if hierarchies don’t change frequently, you could simply store the whole tree in a single document.
  - You might also consider storing the data for each node in its own document, and having an array with references to the parents back to the beginning, and a nested set of arrays listing the children.
  - The approaches can be hybridized considerably based on your needs.
  -  The downside of the document db approach here is that writes may require numerous updates to be complete. However, reads, which are typically the bulk of data access, only require a single operation.

## Key value pairs

- In a relational database this is often done with a three column table, with one column for the related entity, a column for the key, and a column for the value.
  - Type safety here is garbage, as in index performance on the value.
- In a document database, this would simply be stored in a dictionary under the entity document, provided that the data was small in size.
  - If there was a larger amount of data, or if some parts aren’t frequently used, this data could be stored in a different document.
  - In addition to avoiding the type safety and performance issues of the relational model, it’s also easier to store complex types in this structure, without having to serialize json or do odd things with your keys to indicate nesting.

## Sparse tables

- Sometimes entities have a lot of fields, few of which are actually filled in. This can be for a variety of reasons.
- In a relational model, you can do several approaches to this one. Key value pairs, nullable columns, or even multiple other tables for sets of values could be used. All of these approaches have problems – you just pick the problems you can stand to have.
- In a document database, these can just be nullable fields on the document.

## 
