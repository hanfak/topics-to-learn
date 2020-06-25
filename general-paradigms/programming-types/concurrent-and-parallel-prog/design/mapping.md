# Mapping

- The fourth and final stage of our parallel design process is mapping and this is **where we specify where each of the tasks we established will actually execute.**
- Now this mapping stage does not apply if you're only using a single processor system because there's only one place to execute the program or if you're using a system with automated task scheduling.
- So if I'm just writing programs to run on a desktop computer, like the examples we've shown you throughout this course, mapping isn't even a consideration.
- The operating system handles scheduling threads to execute on specific processor cores, so that's out of our hands.
- **Mapping really becomes a factor if you're using a distributed system or specialized hardware with lots of parallel processors for large scale problems**, like in scientific computing applications.
- The usual goal of a mapping algorithm is to minimize the total execution time of the program and there are two main strategies to achieve that goal.
  - You can place tasks that are capable of executing concurrently on different processors to increase the overall concurrency or
  - you can focus on placing tasks that communicate with each other frequently on the same processor to increase locality by keeping them close together.
- In some situations, it might be possible to leverage both of those approaches, but m**ore often they'll conflict with each other, which means the design will have to make trade off**s.
- There's a variety of different load balancing algorithms that use domain decomposition and agglomeration techniques to map task execution to processors.
-  If the number of tasks or the amount of computation and communication per task changes as the program executes, that makes the problem more complex and it may require dynamic load balancing techniques that periodically determine a new mapping strategy.
- Designing a good mapping algorithm is highly dependent on both the program's structure and the hardware it's running on.
- So, to summarize the four step parallel design process we start by taking a problem and partitioning, or decomposing it, into a collection of tasks. Then we evaluate the communication necessary to synchronize and share data between those tasks. After that, we agglomerate, or combine those tasks into groups to increase the program's efficiency with certain hardware in mind. And then finally, those tasks get mapped to specific processors to actually execute.
