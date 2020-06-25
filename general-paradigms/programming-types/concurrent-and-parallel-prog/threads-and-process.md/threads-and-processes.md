# Threads and Processors

- When a computer runs an application, that instance of the program executing is referred to as a process.
  - A process consists of the program's code, its data, and information about its state.
  - Each process is independent, and has its own separate address space in memory.
  - A computer can have hundreds of active processes at once, and an operating system's job is to manage all of them.
- Now, within every process, there are one or more smaller sub elements called threads.
  - These are kind of like tiny processes.
  - Each of those threads is an independent path of execution through the program, a different sequence of instructions, and it can only exist as part of a process.
  - Threads are the basic units that the operating system manages and it allocates time on the processor to actually execute them.
    - To conceptualize the relationship between a process and its threads, think of two processors cooking together in the kitchen as being two threads executing as part of the same process. We both work independently doing our own tasks that contribute to the overall execution of our program.
      - For example, if we are part of a process to make a salad, my thread might handle retrieving vegetables from the pantry and fridge. And the other processor will handle chopping them up.
      - If the program requires other tasks, we might create additional threads to handle those too. "Hey processor 2, Can you make some salad dressing?"
      -  Now our salad making process has three active threads, and when one of those threads finishes executing its instructions. It'll exit and leave the remaining threads to continue what they're doing.
    - Threads that belong to the same process share the processes' address space, which gives them access to the same resources in memory including the program's executable code and data.
    - You can think of the kitchen that our two threads are working in like the shared address space for our process. We both have direct access to the same cookbooks containing our instructions or code, and the ingredients that we're cooking with represents the data and variables we're manipulating.
    - The ability for both of us to use these resources is certainly convenient, and it enables us to easily work together, but it does create the potential to cause problems if we don't coordinate our actions
  - Sharing resources between separate processes is not as easy as sharing between threads in the same process, because every process exists in its own address space.
    -  In this process, our two threads are making a salad, but that other process next-door is running a different program. Those threads are baking a cake.
    - Our variables and data are isolated to this address space, this kitchen, so the threads in the other process can't directly access our salad data.
      - Good, we don't want you healthy salad makers messing with our cake either.
    - There are ways to communicate and share data between processes, but it requires a bit more work than communicating between threads.
      - You have to use system-provided inter-process communication mechanisms like sockets and pipes, allocating special inter-process shared memory space, or using remote procedure calls, w
  - Now, it's possible to write parallel programs that use multiple processes working together towards a common goal, or using multiple threads within a single process. So which is better, using multiple threads or multiple processes?
    - It depends on what you're doing and the environment it's running in, because the implementation of threads and processes differs between operating systems and programming languages.
    - If your application is going to be distributed across multiple computers, you most likely need separate processes for that.
    - But, as a rule of thumb, if you can structure your program to take advantage of multiple threads, stick with using threads rather than multiple processes.
    - Threads are considered lightweight compared to processes, which are more resource intensive. A thread requires less overhead to create and terminate than a process, and it's usually faster for an operating system to switch between executing threads from the same process than to switch between different processes.

# Java

- When you run a Java application, it executes within its own instance of the Java Virtual Machine, or JVM, and the operating system treats that instance of the JVM as its own independent process.
- So, if you run multiple Java applications at the same time, they'll each execute in a separate JVM process with their own independent memory space
