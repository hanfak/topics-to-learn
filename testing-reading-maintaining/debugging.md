# Debugging

- cornerstone of programming
  - Most important skill
  - Helps professional programmers work in a non ideal world
- It is to see into the execution of a program by examining it.
  - For fixing the error
  - For understanding the software which lacks documentation, tests
- To get visibility into the execution of a program you must be able to execute the code and observe something about it.
  - Sometimes this is visible, like what is being displayed on a screen, or the delay between two events.
  - In many other cases, it involves things that are not meant to be visible, like
    - the state of some variables inside the code
    - which lines of code are actually being executed, or
    - whether certain assertions hold across a complicated data structure.
  -  These hidden things must be revealed.
- The common ways of looking into the ‘innards’ of an executing program
  - Using a debugging tool,
  - Printlining
    - Making a temporary modification to the program, typically adding lines that print information out
  - Logging
    - Creating a permanent window into the programs execution in the form of a log.
- Involves changing code to find out what is going on
  - safe doing this using existing tests suite and version control

## Debuggin: Splitting problem space

- IT is a mystery to be solved
  - You think it should do something, but instead it does something else.
- Use divide an conquer to split different areas of code to debug
  - This can be passed to other members of the teams
- Other dimensions of the program, such as
  - the space of executed lines
  - the data structure
  - the memory management
  - the interaction with foreign code
  - the code that is risky
  - the code that is simple

## Removing the error

- In fixing a bug, you want to make the smallest change that fixes the bug.
  - You may see other things that need improvement; but don't fix those at the same time.
- Attempt to employ the scientific method of changing one thing and only one thing at a time
- **The best process for this is to be able to easily reproduce the bug, then put your fix in place, and then rerun the program and observe that the bug no longer exists.**
- Sometimes, there are really several bugs that look like one.
  -

## Debugging tool

- Debugging tools often lag behind language development, so at any point in time they may not be available.
- the debugging tool may subtly change the way the program executes it may not always be practical

### Using IDE

- Break points
  - Handling loops
  - Where to place
    - use stack trace
- debugging through streams
- Go to breakpoint
- next step
- go into
- Evaluate expression
  - code fragment

## Use print statements

- for when app is running in container and cannot debug via IDE

## Stack trace

- Search for exception message
- search for path which involves your code


## Debug using Logs

- Logging is the practice of writing a system so that it produces a sequence of informative records, called a log
- The amount of information that is provided by the log should be configurable, ideally while the program is running
- Beneifts of logs
  - Logs can provide useful information about bugs that are hard to reproduce (such as those that occur in the production environment but that cannot be reproduced in the test environment).
  - Logs can provide statistics and data relevant to performance, such as the time passing between statements.
  - When configurable, logs allow general information to be captured in order to debug unanticipated specific problems without having to modify and/or redeploy the code just to deal with those specific problems.
- The amount to output into the log is always a compromise between information and brevity. Too much information makes the log expensive and produces scroll blindness, making it hard to find the information you need. Too little information and it may not contain what you need.
- Typically, each record in the log will
  - identify its position in the source code
  - the thread that executed it if applicable
  - the precise time of execution,
  - commonly, an additional useful piece of information, such as the value of some variable, the amount of free memory, the number of data objects, etc.
- These log statements are sprinkled throughout the source code, particularly at major functionality points and around risky code
- Each statement can be assigned a level and will only output a record if the system is currently configured to output that level.
- You should design the log statements to address problems that you anticipate

## Debugging performance problems

- Even if you understand perfectly precisely the cost of the code you write, your code will make calls into other software systems that you have little control over or visibility into.
- Before you try to make your system faster, you must build a mental model of why it is slow.
  - can use a profiling tool or a good log/metrics to figure out where the time or other resources are really being spent.
-  Often most of the time is spent in I/O in one way or another. Finding the expensive I/O
- There are many dimensions to the performance of a computer system, and many resources consumed.
  - The first resource to measure is wall-clock time, the total time that passes for the computation.
    - can inform about unpredictable circumstances that arise in situations where other profiling is impractical
    - may not always represent the whole picture
      - Sometimes something that takes a little longer but doesn't burn up so many processor seconds will be much better in the computing environment you actually have to deal with.
  - memory, network bandwidth, database or other server accesses may, in the end, be far more expensive than processor seconds.
  - Contention for shared resources that are synchronized can cause deadlock and starvation.
    - Deadlock is the inability to proceed because of improper synchronization or resource demands.
    - Starvation is the failure to schedule a component properly

### Fixing

- Intermittant bugs
  - This nightmare occurs so rarely that it is hard to observe, yet often enough that it can't be ignored. You can't debug because you can't find it
  - What makes it hard is that it occurs only under unknown conditions
    - Try to record the circumstances under which the bug does occur, so that you can guess what the variability really is.
    - The condition may be related to data values
    - If that is not the source of variability, the next suspect should be improperly synchronized concurrency.
  - try to reproduce the bug in a controlled way.
    - If you can't reproduce it, set a trap for it by building a logging system, a special one if you have to, that can log what you guess you need when it really does occur.
      - Necssary if bug only found in production
      - But takes a long time
  - This can happen in third party code

## Debugging while container is up

- https://medium.com/swlh/remote-debugging-a-java-application-running-in-docker-container-with-intellij-idea-efe54cd77f02
