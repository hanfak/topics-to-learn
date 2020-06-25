# Concurrent and parallel programming

- Just because a program is structured to have multiple threads or processes does not mean they'll necessarily execute in parallel.
- Concurrency and parallel excution are not the same
- **Concurrency refers to the ability of an algorithm or program to be broken into different parts that can be executed out of order or partially out of order without affecting the end result.**
  -  Concurrency is about how a program is structured and the composition of independently executing processes.
  - Consider this recipe to make a salad, which includes several steps that involve slicing and chopping vegetables.
    - We can decompose those steps into a collection of concurrent tasks because the relative order in which we do them doesn't matter.
    - They're order independent.
    - To keep things simple, let's just focus on two of those tasks for now.
      - I'll chop onions and someone else slice cucumbers.
      - This knife represents our computer's processor.
      - We only have one knife, so this is a single core processor.
      - And only one of us will be able to execute our vegetable chopping routine at any given time.
        - Each operation will have to take turns.
        - My thread will use a processor to execute and slice some cucumbers. Then, after a bit, we'll swap places. Someone elses thread gets some time to execute and slice onions.  Swapping places again, and will keep on doing this until both operations are done.
        - In this scenario, we're running concurrently because our two independent processes overlap in time.
      - However, since we only have a single processor, only one of us will actually be executing at any instant in time.
        - If we swap places and take turns more frequently, it might create the illusion that we're executing simultaneously on our single processor, but this is not true parallel execution.
      - To actually execute in parallel, we need parallel hardware.
        - In our kitchen, that means another knife and cutting board, a second processor.
        - But in regards to computers, parallel hardware can come in a variety of forms.
          - Most modern processors used in things like desktop computers and cellphones have multiple processing cores. Graphics processing units, or GPUs, contain hundreds, or even thousands, of specialized cores working in parallel to make amazing graphics that you see on the screen.
          - And computer clusters distribute their processing across multiple systems.
          - Since we've structured ourselves as concurrent operations, I can begin slicing cucumbers with this processor. While someone else cut onions with the other one. Now we're actually executing in parallel because we're both executing at the same time. And, as a result, we're able to finish the job faster.
  - **Concurrency is about the structure of a program, being able to deal with multiple things at once**
  - **parallelism is about simultaneous execution, actually doing multiple things at once.**
  - Those things could be related, like chopping vegetables, but they don't have to be.
  - Concurrency enables a program to execute in parallel, given the necessary hardware.
  - But a concurrent program is not inherently parallel.
  - Programs may not always benefit from parallel execution.
    - For example, the software drivers that handle I/O devices, like a mouse, keyboard, and hard drive, need to execute concurrently. They're managed by the operating system as independent things that get executed, as needed. In a multi-core system, the execution of those drivers might get split amongst the available processors.
    - However, since I/O operations occur rather infrequently, relative to the speed at which computer operates, we don't really gain anything from parallel execution.
    - Those sparse independent tasks can run just fine on a single processor, and we wouldn't feel a difference.
  - **Concurrent programming is useful for I/O-dependent tasks** like graphical user interfaces.
    - When the user clicks a button to execute an operation, that might take a while.
    - To avoid locking up the user interface until it's completed, we can run the operation in a separate concurrent thread.
    - This leaves the thread that's running the UI free to accept new inputs.
  - Parallel processing really becomes useful for computationally intensive tasks,
    - such as calculating the result of multiplying two matrices together.
    - When large math operations can be divided into independent subparts, executing those parts in parallel on separate processors can really speed things up.

## Links

- https://howtodoinjava.com/java/multi-threading/concurrency-vs-parallelism/
- http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html
- https://stackoverflow.com/questions/1050222/what-is-the-difference-between-concurrency-and-parallelism
