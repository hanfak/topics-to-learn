# Data structures

- Most languages provide two types of containers:
  - Sequential containers store objects at a particular position, denoted by a numerical index.
  - Associative containers use the object itself to determine where the object should be stored inside the collection.
- For certain contianer methods to work, the objects must have implement some form comparability and equivalence (equals() and hashcode())
- The object is not store in the container, it is the reference to the object
- The Collections API defines a set of interfaces specifying the operations a container of that type must conform to


- Mutable collections which allow mutation of their state in place
  - he majority of standard collections from java.util.
  - When you add or remove elements there, you get the changes at all places which keep a reference to the collection instance.
- Persistent collections are the collections, which persist their previous state when mutation operation is applied on them.
  - When you apply mutation operation on such collection, you get a new independent instance of it, with updated content.
  - Such characteristic makes them effectively immutable.
  - There are plenty different implementations of persistent collections in Java ecosystem.
  - External libraries such as Vavr

- What is it?
  - https://en.wikipedia.org/wiki/Data_structure
  - https://www.geeksforgeeks.org/data-structures/
  - https://medium.com/swlh/introduction-to-data-structures-9134b7d064a6
  - https://www.youtube.com/watch?v=DuDz6B4cqVc
  - https://medium.freecodecamp.org/10-common-data-structures-explained-with-videos-exercises-aaff6c06fb2b

## Contents

- Arrays
- List/ArraysList
- Map/HashMap

## Links

- https://dzone.com/articles/java-collections-part-1?utm_medium=feed&utm_source=feedpress.me&utm_campaign=Feed:%20dzone%2Fjava
