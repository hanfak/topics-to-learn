# AVL Trees 

## Defunct 

- Due to complexity, multiple restructing on insertion and deletion, a RED-BLACK tree is used nowadays

## Uses 

AVL trees are mostly used for in-memory sorts of sets and dictionaries.

AVL trees are also used extensively in database applications in which insertions and deletions are fewer but there are frequent lookups for data required.

It is used in applications that require improved searching apart from the database applications.

AVL tree is a balanced binary search tree which employees rotation to maintain balance.

It has application in story-line games as well.

It is use mainly used in corporate sectors where the have to keep the information about the employees working there and their change in shifts.

When searches are more numerous than mutating operations

## pros 

The height of the AVL tree is always balanced which means the height never grows beyond log N, where N is the total number of nodes in the tree.

It gives better search time complexity when compared to simple Binary Search trees.

AVL trees have self-balancing capabilities.

## cons 

As we can see from above examples, AVL trees can be difficult to implement.

In addition to that, AVL trees have high constant factors for some operations.

This rotation mechanism is time consuming, so when your job is mostly insertion than searching then AVL tree is not efficient

Most STL implementations of the ordered associative containers (sets, multisets, maps and multimaps) use red-black trees instead of AVL trees. Unlike AVL trees, red-black trees require only one restructuring for a removal or an insertion.