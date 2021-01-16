# Map

-  is an interface that maintains key-to-value relationships, and retains only unique keys
- If the same key and different value is added to a map, the old value is replaced by the new value.
- Implementations
  - hashmap
  - treemap
  - LinkedHashMap
- Other languages call it a dictionary

## HashMap

- hash table, but with a few additional embellishments
- Initially the bucket entries will be stored in a list.
- When it comes to finding a value, the hash of the key is calculated and then the equals() method is used to find the key in the list.
  - Because of the mechanics of hashing the key and using equality to find it in the list, duplicate keys are not permitted in a HashMap.
  - Inserting the same key simply replaces the key currently stored in the HashMap.
- initialCapacity and loadFactor affect performance
  - can be set via constructor args
  - The capacity of a HashMap represents the current number of buckets that have been created, which defaults to 16.
    - An accurate initialCapacity will avoid the need to automatically rehash as the table grows.
  - The loadFactor represents how full the hash table is allowed to get before the capacity is automatically increased.
    - Increasing the capacity and recalculating hashes is a procedure known as rehashing, which doubles the number of buckets available and redistributes the data stored.
    - It is also possible to tweak loadFactor, but 0.75 (the default) provides a good balance between space and time of access.
    - A loadFactor of higher than 0.75 will reduce the rehashing requirement, but access will become slower as buckets will generally become fuller
    - Setting the initialCapacity to the maximum number of elements divided by the loadFactor will prevent a rehash operation from occurring.
- operations
  - constant-time support for get() and put() operations, but iteration can be costly.
    - high loadfactor and initialcapacity can impact iteration
- Treeifying
  - internal aspect of hashmap
  - when a bucket becomes highly populated. If the bucket elements are implemented as a LinkedList, traversal to find an element becomes on average more expensive as the list grows.
  - To reduce this linear affect, the bucket turns from list to tree (treeenodes), when the treeifying_threshold is reached
  - This is not done at the beginning
    - tree nodes are double the size of list nodes
    - A well-distributed hashing function will rarely cause buckets to be converted to TreeNodes.
  - If this happens needs to change initialCapacity and loadFactor

## Links

- https://beginnersbook.com/2013/12/hashmap-in-java-with-example/
- https://www.javacodegeeks.com/2017/11/java-hashmap-detail-explanation.html
- https://dzone.com/articles/how-to-use-java-hashmap-effectively
