# Arraylist vs Linkedlist

- Linked list is more dynamice than arraylist, it does not have to resize and copy over the elements
  - Thus appending(adding element to the end) is O(1)
- Depends on access or modification of container
  - Inserting at the end of a list in both ArrayList (initialized sized) and LinkedList is a constant-time operation
  - Insertion with in container
    - ArrayList requires all other elements to be shifted by one position to the right.
    - LinkedList has to traverse node references to find the position in the list where the insert is required, but the insert itself simply involves creating a new node and setting two references, one pointing to the node at the beginning of the list (the first reference) and the other to the next node in the list (the next reference).
      - Far more performant
  - List removal has a similar behavior
    - it is cheaper to remove from a LinkedList, at most two references need to change.
    - In an ArrayList, all items to the right of the deletion need to shift one place to the left.
  - Random Read
    - randomly ArrayList is the best choice, as any element can be accessed in O(1) time
    - LinkedList requires navigation from the beginning to the index count
- In general it is recommended to prefer ArrayList unless you require the specific behavior of LinkedList, especially if you are using an algorithm that requires random access.
- https://stackoverflow.com/questions/322715/when-to-use-linkedlist-over-arraylist-in-java
