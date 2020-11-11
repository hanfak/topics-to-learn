# How to Optimize Loops

- Sometimes you'll encounter loops, or recursive functions, that take a long time to execute and are bottlenecks in your system
- First, search for a way of removing the loop entirely before looking to optimise
- Recursion, can lead to code being more complex and harder to understand, if you value development performance over system performance then consider replacing these
  - use of functinoal ways, ie streams, lambdas might be better
- Optimising loops
  - Move as much stuff out of the loop, so actions are not repeated
    - Example
      - Remove floating point operations.
      - Don't allocate new memory blocks unnecessarily.
      - Fold constants together.
      - Move I/O into a buffer.
      - Try not to divide.
      - Try not to do expensive typecasts.
      - Move a pointer rather than recomputing indices.
      - String creation
  - If you are looping of data in memory, but this came from a database, instead of doing it in code, let the database do it for you (it is optimised to handle this)
  - These can be language specific
