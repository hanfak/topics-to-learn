# Depth First Search

- Used on graphs

## Use cases

- Detecting cycle in a graph
  - A graph has cycle if and only if we see a back edge during DFS. So we can run DFS for the graph and check for back edges.
- We can specialize the DFS algorithm to find a path between two given vertices u and z.
  - i) Call DFS(G, u) with u as the start vertex.
  - ii) Use a stack S to keep track of the path between the start vertex and the current vertex.
  - iii) As soon as destination vertex z is encountered, return the path as the contents of the stack
- Topological Sorting
  - Topological Sorting is mainly used for scheduling jobs from the given dependencies among jobs. In computer science, applications of this type arise in instruction scheduling, ordering of formula cell evaluation when recomputing formula values in spreadsheets, logic synthesis, determining the order of compilation tasks to perform in makefiles, data serialization, and resolving symbol dependencies in linkers
- To test if a graph is bipartite
  - We can augment either BFS or DFS when we first discover a new vertex, color it opposite its parents, and for each other edge, check it doesn’t link two vertices of the same color. The first vertex in any connected component can be red or black
- Finding Strongly Connected Components of a graph A directed graph is called strongly connected if there is a path from each vertex in the graph to every other vertex.
- Solving puzzles with only one solution, such as mazes.
  - DFS can be adapted to find all solutions to a maze by only including nodes on the current path in the visited set.
  - decision trees
- When the tree is very wide (has a lot of branches)
-  find the longest path between two nodes in a graph.
- visit child nodes before sibling nodes.
