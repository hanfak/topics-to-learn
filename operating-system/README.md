# Operating Systems

Information about using

- Linux
- Bash
- Scripting
- etc

## What is an Operating System?

- An Operating System (OS) is a collection of software that manages computer hardware and provides services for programs.
  - it hides hardware complexity,
  - manages computational resources
  - provides isolation and protection.
  - it directly has privilege access to the underlying hardware.
- Major components of an OS are
  - the file system
  - scheduler
  - device driver.
- three key elements of an operating system
  - (1) Abstractions (process, thread, file, socket, memory)
  - (2) Mechanisms (create, schedule, open, write, allocate)
  - (3) Policies (LRU, EDF)
- two operating system design principles
  - (1) Separation of mechanism and policy by implementing flexible mechanisms to support policies
  - (2) Optimization for common case:
    - Where will the OS be used?
    - What will the user want to execute on that machine?
    - What are the workload requirements?
- three types of Operating Systems commonly used nowadays.
  - Monolithic OS
    - where the entire OS is working in kernel space and is alone in supervisor mode.
  - Modular OS
    - in which some part of the system core will be located in independent files called modules that can be added to the system at run time.
  - Micro OS
    - where the kernel is broken down into separate processes, known as servers. Some of the servers run in kernel space and some run in user-space.

## Concepts of Operating systems

- Processes and Process Management
- Threads and Concurrency
- Scheduling
- Memory Management
- Inter-Process Communication
- Input/Output Management
- Virtualization
- Distributed File Systems
- Distributed Shared Memory
- Cloud Computing
