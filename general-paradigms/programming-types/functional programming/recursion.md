# Recursion

- https://www.freecodecamp.org/news/how-recursion-works-explained-with-flowcharts-and-a-video-de61f40cb7f9/

## Disadvantages of recursion

- Issues with stackoverflow errors
  - Java has no Tail Call optimization (yet), hence yes, recursive solutions may give you StackOverflowError.
- performance loss as it has to create new stack frame and do some other stuff for each recursive invocation.
- Readability might be harder
- Harder to debug
- using recursion can also restrict you from using concurrency to speed up parallel operations. 
- https://stackoverflow.com/questions/41469031/is-recursion-a-bad-practice-in-general
-
