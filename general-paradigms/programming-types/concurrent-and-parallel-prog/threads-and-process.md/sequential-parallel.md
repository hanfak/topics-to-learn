# Sequential computing

- Implementing a list of instructions in a sequential manner
  - 1 -> 2 -> 3 -> .... -> n
- One processor, doing all the jobs, in discrete instructions, in order
  - Only doing one instruction at any given moment
  - Must wait for current instruction/operation to complete before starting the next one
- Known as serial programming
- Limitations
  - Time taken to complete is limited by
    - the speed of the processor
    - how fast it can execute that series of instructions.
  - Once all steps are optimised, cannot improve upon this time
  - Only execute one instruction at a time
  - If series of operations, in method or api call, takes 1 min to perform, then 10000 calls will take 10000 minutes (166 hours, 7 days). This is a problem when you need to have done all these calls within a couple of hours ie for another task to start.

# Parallel computing

- To complete a set of instructions using multiple processes
  - processor one: 1 -> 4 -> 6
  - processor two: 2 -> 3 -> 5
  - When both processes are finished then the operation is finished
  - If all steps were independent then we can do them in any order
    - processor one: 1 -> 3-> 6
    - processor two: 2 -> 4 -> 5
  - If a Step 7 required 5 and 6 to be completed then we go back to serial computing
    - which means both processors need to coordinate to make sure both have finised step 5 and 6 befor starting step 7
- Working in parallel
  - we've broke the operation into independent parts that can be executed simultaneously by different processors.
  - This increases the time it took to complete the process
  - Good for independent operations that dont depend on each other
- Having more processes, does not mean it will improve the time by the factor of number of processes
  - More processors adds complexity
  - Each proceessors will increase number of times need to coordinate with each other
  - there will be wait times, for one processor to finsih before continuing on in a sequential manner
-  parallel execution increases the overall throughput of a program,
  - enabling us to break down large tasks to accomplish them faster or
  - to accomplish more tasks in a given amount of time
- Some tasks are impossible to solve using one processor

## Parallel hardware

- Parallel computing requires parallel hardware
  - multiple processors to execute different parts of a program at the same time
- Classifying multiple processor technologies
  - flynns taxonomy
    - which distinguishes four classes of computer architecture based on two factors, the number of concurrent instruction or control streams, and the number of data streams
      - The simplest of these four classes is the Single Instruction, Single Data or SISD architecture, which is a sequential computer with a single processor unit.
        - If I am an SISD computer, at any given time, I can only execute one series of instructions, such as chopping, and I can only act on one element of data at a time, this carrot. (chopping) - It's simple, like an old computer.
      - Single Instruction, Multiple Data, or SIMD, which is a type of parallel computer with multiple processing units.
        - All of its processors execute the same instruction at any given time, but they can each operate on different data element.
        - As an SIMD computer, our two processors are both executing the same chopping instruction, but I'm chopping celery as my data while another processor chops a carrot. - And we'll execute those instructions in sync with each other. (chopping)
        - This type of SIMD architecture is well-suited for applications that perform the same handful of operations on a massive set of data elements like image processing.
        - And most modern computers use graphic processing units or GPUs with SIMD instructions to do just that.
      - Our third class is the opposite of SIMD. In a Multiple Instruction, Single Data or MISD architecture, each processing unit independently executes its own separate series of instructions.
        - However, all of those processors are operating on the same single stream of data.
          - That's like a processor executing the chopping instruction while I execute a different, peeling instruction, but we're both chopping and peeling the same carrot at the same time. - Yeah we're not doing that.
          - As you can see, MISD doesn't make much practical sense, so it's not a commonly used architecture.
      - In a Multiple Instruction, Multiple Data or MIMD computer, every processing unit can be executing a different series of instructions, and at the same time, each of those processors can be operating on a different set of data.
        - Now, I can slice celery while another processor peels carrots. (chopping and peeling)
        - MIMD is the most commonly used architecture in Flynn's taxonomy, and you'll find it in everything from multicore PCs to network clusters and supercomputers.
        - Now, that broad MIMD category is sometimes further subdivided into two parallel programming models, which also have four letter names.
          - Single Program, Multiple Data, or SPMD, and Multiple Program, Multiple Data, MPMD.
          - In the SPMD model, multiple processing units are executing a copy of the same single program simultaneously.
            - However, they can each use different data. That might sound a lot like the SIMD architecture from earlier, but it's different because although each processor is executing the same program, they do not have to be executing the same instruction at the same time.
            - The processors can run asynchronously and the program usually includes conditional logic that allows different tasks within the program to only execute specific parts of the overall program.
            - If both processors are both following the same recipe or program, I can execute part of it, while another processor handles a different task.
            - This SPMD model is the most common style of parallel programming and when we show you programming examples later in this course, we'll structure the code as a single program and execute it on a multicore desktop computer, which is an MIMD architecture.
          - Now, if each of our processors is executing a different recipe, that represents the Multiple Program, Multiple Data or MPMD model.
            - In this scenario, processors can be executing different, independent programs at the same time while of course also be operating on different data.
            - Typically in this model, one processing node will be selected as the host or manager, which runs one program that farms out data to the other nodes running a second program. Those other nodes do their work and return their results to the manager.
            - MPMD is not as common as SPMD, but it can be useful for some applications that lend themselves to functional decomposition, which we'll cover later on.
- hyper-threading, which enables cores to each run two independent applications at the same time so that the computer, those 12 physical cores, are treated as 24 logical processors
  - hyper-threading in those 12 cores does not mean I'll get double the performance out of them. Hyper-threading takes advantage of unused parts of the processor, so if one thread is paused or not using a certain resource, then the other thread may be able to use it. So under certain workloads, that can create performance improvements, but it's highly application dependent.

## Shared and distributed memory

- How memory is organised and accessed
  - you could put a billion processors in a computer but if they cant access memory fast enough to get the instructions and data they need, then you won't gain anything from having all those processors.
- Computer memory usually operates at a much slower speed than processors do and when one processor is reading or writing to memory, that often prevents any other processors from accessing that same memory element.
- There are two main memory architectures that exist for parallel computing, shared memory and distributed memory.
- In a shared memory system, all processors have access to the same memory as part of a global address space.
  - Although each processor operates independently, if one processor changes a memory location, all of the other processors will see that change.
  - So if I change something in our shared memory space. (thumps) - Hey, that potato is two potatoes. - Every other processor sees that change too.
  - shared memory doesn't necessarily mean all of this data exists on the same physical device. It could be spread across a cluster of systems.
    - The key is that both of our processors see everything that happens in the shared memory space.
  - Shared memory is often classified into one of two categories, uniform memory access, and nonuniform memory access, which are based on how the processors are connected to memory and how quickly they can access it.
    - In a uniform memory access or UMA system, all of the processors have equal access to the memory, meaning they can access it equally fast.
    - There are several types of UMA architectures, but the most common is a symmetric multiprocessing system or SMP.
      - An SMP system has two or more identical processors which are connected to a single shared memory often through a system bus.
      - In the case of modern multicore processors, which you find in everything from desktop computers to cell phones, each of the processing cores are treated as a separate processor.
  -  Now, in most modern processors, each core has its own cache, which is a small, very fast piece of memory that only it can see, and it uses it to store data that it's frequently working with.
    - However, caches introduce the challenge that if one processor copies a value from the shared main memory, and then makes a change to it in its local cache, then that change needs to be updated back in the shared memory before another processor reads the old value, which is no longer current.
    -  This issue, called cache coherency, is handled by the hardware in multicore processors.
    - The other type of shared memory is a nonuniform memory access or NUMA system, which is often made by physically connecting multiple SMP systems together.
      - The access is nonuniform because some processors will have quicker access to certain parts of memory than others.
      - It takes longer to access things over the bus. But overall, every processor can still see everything in memory.
      - These shared memory architectures have the advantage of being easier for programming in regards to memory, because it's easier to share data between different parts of a parallel program.
      - The downside is that they don't always scale well. Adding more processors to a shared memory system will increase traffic on the shared memory bus, and if you factor in maintaining cache coherency, it becomes a lot of communication that needs to happen between all the parts.
      - In addition to that, shared memory puts responsibility on the programmer to synchronize memory accesses to ensure correct behavior,
  - In a distributed memory system, each processor has its own local memory with its own address space, so the concept of a global address space doesn't exist.
    - All the processors are connected through some sort of network, which can be as simple as Ethernet.
    - Each processor operates independently, and if it makes changes to its local memory, that change is not automatically reflected in the memory of other processors.
    - If I make a change to the data in my memory, (chops) another processor is oblivious to that change. It's up to the programmer to explicitly define how and when data is communicated between the nodes in a distributed system, and that's often a disadvantage.
      - Communication is always tough.
    - The advantage of a distributed memory architecture is that it's scalable.
      -  When you add more processors to the system, you get more memory too.
      - This structure makes it cost-effective to use commodity, off-the-shelf computers, and networking equipment to build large distributed memory systems.
      - Most supercomputers use some form of distributed memory architecture or a hybrid of distributed and shared memory.
