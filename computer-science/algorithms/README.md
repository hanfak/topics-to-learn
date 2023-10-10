# Algorithms

## Notes

- http://www.catonmat.net/blog/mit-introduction-to-algorithms-part-one/
- https://monami555.github.io/2017/02/19/algorithms-revision.html
- https://github.com/enkidevs/curriculum/wiki/Comp.-Sci.-Data-Structures-and-Algorithms-Course
- https://yangshun.github.io/tech-interview-handbook/algorithms/algorithms-introduction/
- https://www.freecodecamp.org/news/tree-traversals-explained-theyre-like-a-class-of-lazy-students-trying-to-cheat-on-their-exam-b46563211427/
- https://github.com/makersacademy/course/tree/main/algorithmic_complexity
- https://www.quora.com/Do-programmers-really-have-to-know-how-to-calculate-the-big-O-for-their-programs
- https://www.piratekingdom.com/leetcode/templates
## courses

- https://www.jomaclass.com/data-structures-and-algorithms
  - https://www.youtube.com/watch?v=oz9cEqFynHU
- https://inst.eecs.berkeley.edu/~cs61b/sp20/
  - https://www.youtube.com/playlist?list=PLu0nzW8Es1x3TmpwQRLMQwCtulEd43ZY8
- https://www.khanacademy.org/computing/computer-science/algorithms

## Topic

1. Logarithm (Complexity Analysis)
2. Graph Traversals (BFS & DFS)
3. Binary Search
4. Sliding Window
5. Recursion
6. 2 Algorithms (Inverting a binary tree & Reverse a Linked List)
7. Suffix Trees
8. Heaps
9. DP
10. Sorting Algorithms (Quick & Merge)

## Usage 

- https://youtu.be/7VHG6Y2QmtM Big O myths busted! (Time complexity is complicated)
  - how to determine the best algorithm and explains that comparing algorithms involves considering factors such as time complexity.
  - the importance of starting with a simple, working solution.
  - The performance of the algorithm is analyzed by benchmarking it
  - Need to discover where the  bottleneck is with evidence rather than guesswork 
  - Big O notation to describe algorithmic time complexity and explains that it focuses on the shape of the performance chart rather than specific numbers or constant factors.
  - Figuring out best and worst case scnearios
  - analyzing the loop bounds is essential for determining the time complexity of an algorithm.
  - importance of stress testing algorithms is highlighted to evaluate their performance in real-world scenarios.
  - Trying different alogrithms are needed so that they can be compared
  - Each algorithm will have a their own trade off
  - real-world hardware performance may differ from theoretical time complexity, and optimization efforts can impact the actual execution time.
    - Optimising may also be counter productive due to compiler and JIT
  - Memory usage can have an impact too
    - ie Doing a look up with a hash table, is fast, but set up or updating the hash table is slow. 
      - Choice of reads is greater than writes (or write once) this will be ideal
  - pre processing data can improve performance for certain parts but reduce performance in an earlier stage 
    - Pre-processing data refers to the act of preparing or organizing the data in a specific way before performing any operations or computations on it.
    - it allows the algorithm to access and manipulate the data more efficiently during runtime. By organizing the data in a way that suits the specific needs of the algorithm, it reduces the amount of work required during the actual execution of the algorithm.
    - can also involve performing calculations or generating intermediate results in advance, which are then used during the actual execution of the algorithm.
    - This eliminates the need to repeat these calculations for each individual operation, reducing redundant work 
  - Can take advantage of hardware, using techniques like Single Instruction Multiple Data (SIMD)
    - perform the same operation on multiple data elements simultaneously. It is specifically designed to optimize performance for tasks that involve parallel processing
  - instead of processing one data element at a time, SIMD enables the processing of multiple data elements simultaneously using a single instruction.
  - 

