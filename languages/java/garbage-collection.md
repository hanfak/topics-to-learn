# Garbage Collection

- Essential part of java/jvm
- Before programmers had little choice but to track all the memory
they’d allocated manually, and deallocate it once nothing was using it
anymore
  - use of malloc
  - This is hard
  - requires discipline
  - manual deallocation is a frequent cause of memory leaks (if too late) and crashes (if too early)
- Modern GC, can be faster than manually handling memory
  - Correct algorithms can make allocation efficient by reducing fragmentation and contention
  - can make allocation efficient by reducing fragmentation and contention
- Object location in memory matters
  - A high proportion of a program’s execution time is spent stalled in hardware, waiting for memory access.
  - Heap access is geologically slow compared to instruction processing, so modern computers use caches
  -  When an object is fetched into a processor’s cache, its neighbors are also brought in, if they happen to be accessed next, that access will be fast
  -  Having objects that are used at the same time near each other in memory is called object locality, and it’s a performance win.
  -  benefits of efficient allocation
    -  If the heap is fragmented, when a program tries to create an object, it will have a long search to find a chunk of free memory big enough, and allocation becomes expensive
    -  you can force GC to compact more; it will massively increase GC overhead, but often application performance will improve.
-  JVM GC algorithms
  -  Choice can has trade offs, like throughput may be traded off against latency, and workloadaffects the optimum choice.
  -  Stop-the-world collectors halt all program activity so they can collect safely.
  -  Concurrent collectors offload collection work to application threads, so there are no global pauses; instead, each thread will experience tiny delays.
    -  concurrent collectors are less efficient than stop-the-world ones, so they’re suitable for applications where pauses would be noticed ie gui/music playback
  -  Collection itself is done by copying or by marking and sweeping.
    -  the heap is crawled to identify free space, and new objects get allocated into those gaps.
    - Copying collectors divide the heap into two areas. Objects are allocated in the “new space.” When that space is full, its nongarbage contents are copied to the reserve space and the spaces are swapped.
    - In a typical workload, most objects die young (this is known as the generational hypothesis). With shortlived objects, the copying step will be super fast (there’s nothing to copy!). However, if objects hang around, collection will be inefficient. Copying collectors are great for immutable objects and a disaster with object pooling “optimizations”
    -  copying collectors compact the heap, which allows near-instant object allocation and fast object access (fewer cache misses)
