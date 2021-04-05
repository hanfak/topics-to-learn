# Other Collections

- They constitute one of the basic building blocks of commonly developed code
- Most use ArrayList as the default, but there are different collections which might be better suited for your needs
- Collections can be classified as ordered or unordered.
  - Ordered collections have a predictable iteration order;
  - unordered collections do not have a predictable iteration order
- Collections are sorted or unsorted.
  - The elements in a sorted collection are sequenced from start to end based on a comparator;
  - unsorted collections have no particular sequence based on elements
- ordered collections have a predictable iteration order but no sort order
- Sorted collections have a predictable sort order, hence they have a predictable iteration order.
- **all sorted collections are ordered collections, but not all ordered collections are sorted collections**
- Examples
  - List
    - is an interface for ordered collections with a stable indexing order
    - allows duplicate elements to be inserted and provide a predictable iteration order
    - implementations like ArrayList and LinkedList
    - To find a particular element, the contains method can be used.
      - The contains operation traverses the list from the beginning, hence finding elements in a List is an O(n) operation.
  - Map
    - is an interface that maintains key-to-value relationships, and retains only unique keys
    - If the same key and different value is added to a map, the old value is replaced by the new value.
    - implementations like
      - HashMap
        - unordered
        - rely on hashCode and equals to determine unique keys.
      - LinkedHashMap
        - ordered
        - rely on hashCode and equals to determine uniquekeys.
      - TreeMap
        - sorted: the keys are sorted according to a comparator or by the sort order of Comparable keys.
        - relies on compareTo to determine sort order and uniqueness of keys
    - To find a particular element, Map provides the containsKey and containsValue methods
      -  HashMap, containsKey looks up the key in the internal hash table. If the look-up results in a non-null object, it is checked for equality with the object passed to containsKey.
      - The containsValue operation traverses all the values from the beginning.
      - Hence, finding keys in a HashMap is an O(1) operation, whereas finding values in a HashMap is an O(n) operation
  - Set
    - is an interface for collections of unique elements
    -  sets are backed by maps where the keys are the elements and values are null
    - implementations like HashSet (backed by HashMap), LinkedHashSet (backed by LinkedHashMap), and TreeSet (backed by TreeMap).
    - The contains method on a Set delegates to containsKey of a Map and therefore is an O(1)
  -

Basic collections see

## unmodifiable equivalents

## Linked list

## Linked list hash map

## Queues

- https://dzone.com/articles/the-developers-guide-to-collections-queues


## Stacks


## Sets

- https://dzone.com/articles/the-developers-guide-to-collections-sets


## Collections

- https://dzone.com/articles/a-deep-dive-into-collections

## Vector

## Links

- https://www.java67.com/2013/08/ata-structures-in-java-programming-array-linked-list-map-set-stack-queue.html
- Java docs about Collections library: https://docs.oracle.com/javase/8/docs/technotes/guides/collections/designfaq.html
