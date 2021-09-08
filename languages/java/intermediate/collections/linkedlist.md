# Linked List

## What

- An implementation of List interface
  - implement double linked list
- Each element has a reference to the next element
  - For double linked list, an element has a reference to next and the element that links to it

## When to use linked list

- Avoid
  - random access since the list must iterate internally to reach the required position
  - positional add and remove have linear time complexity, on average.

- used
  - LinkedList does have a performance advantage over ArrayList is in adding and removing elements anywhere other than at the end of the list, which is constant time
  - your application needs to frequently insert and remove elements near the start of the list as part of a process that uses iteration, LinkedList may be better.

- https://stackoverflow.com/questions/322715/when-to-use-linkedlist-over-arraylist-in-java

## Common operations
