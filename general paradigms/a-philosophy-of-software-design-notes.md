## From you tube talk

https://www.youtube.com/watch?v=bmSAYlu0NcY

course : https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lectures.php

https://lethain.com/notes-philosophy-software-design/

- Most important concept in this field is decomposition of a problem and build it relatively easily.
- Idea of software design is doing things today to make it easier to develop in the future
-  One thing that determines high and low performers is practise
- Iterative process of building a system, use code reviews to edit and improve, then build from scratch
- General list
  - Working code is not enough, must minimise complexity
  - complexity comes from dependencies and obscruity
  - strategic vs tactical Programming
  - Classes should be deep
  - General purpose classes are deeper
  - new layer new abstraction
  - Comments should describe things that are not obvious from the code
  - Define errors out of existance
  - pull complexity downwards
- Class should not have large interface or lots of dependencies or side effects (this is the complexity) and not much funcitionality (impementation)
- Class should have small interface and deep functionality.
  - Apply to methods/classes/modules
- Shallow classes are an example of just calling another dependency's method
  - Issue with advice that classes/methods should be small, this  leads to shallow classes
  - EG filestream, buffered stream in java library. Need to create lots of objects instead of using one object
  - IT is not about length of class, it is about lots of abstractions
- Example of deep interface, Unix file i/o, wiht five methods
  - Lots of implementation details hidden

- Define errors out of existence
  - https://web.stanford.edu/~ouster/cgi-bin/cs190-winter18/lecture.php?topic=exceptions
  - Huge source of complexity
  - Common wisdom: detect and throw as many exceptions
  - OVerall goal: minimise number of places where exceptions must be handled
  - Aim redefine the exception, so it does not exist, make normal behavour do the right things
    - ie java substring, throws lots of exceptions, instead better to return empty string if some error, if indexs are wrong sort it out (use correctly)
  - program defensively, but dont let exceptions be thrown
  - WHat matters in throwing an exception
  - Best to throw exceptions isntead of error code if it is propagate up, if caught immediately then use error code.
  - Crashing best for out of memory exceptions, to hard to catch
- Tactical vs strategic (mindset)
  - wrong approach is tactical
    - results in bad design, high complexity
    - quick fixes, shortcuts
    - short termism, get it working
    - problems start off small, and become speghetti exponentially
  - Workign code is not enough
  - Strategic
    - goal: produce great design
    - simplify future dev
    - minimise complexity
    - must sweat the small stuff
    - Take extra time today, will pay off in future
  - Complexity is inevitable, can slow it down
  - Most startups are tactical
    - get product out as fast as possible
    - hard to repair
    - Facebook
      - move fast break things
      - unstable hard to use codebase
      - mantra change to move fast with solid infrastructure
  - Get product out fast is to get best programmers, programmers want to work with clean code bases
  - How much to invest
    - 10 -20 %
    - Make small changes
      - For new codebase
        - careful design
        - good documentation
      - existing codebase
        - look for improvements
        - dont settle for few modified lines of code
        - Goal: After change, system should be the way it would have been if designed from the start
  - Layers are good for handling abstraction
    - problem is having too many skinny layers

Quotes

- Complexity is anything that makes software hard to understand or to modify.
- Isolating complexity in places that are rarely interacted with is roughly equivalent to eliminating complexity.
- Complexity is more apparent to readers than to writers. If other people think a piece of code is complex, it is.
- Change amplification is when making a local change requires many changes elsewhere, and is best prevented when you reduce the amount of code that is affected by each design decision, so design changes don't require very many code modifications.
- Complexity is caused by obscurity and dependencies.
- Dependency is when code can't be understood in isolation.
- Obscurity is when important information is not obvious.
- This can often be due to lack of documentation.
- Complexity is incremental, the result of thousands of choices. Which makes it hard to prevent and even harder to fix
- Tactical mindset is focused on getting something working, but makes it nearly impossible to produce good system design.
- Strategic programming is realizing that working code isn't enough. The primary goal is a good design that also solves your problem, not working code.
- you should be doing lots of incremental design improvement work over time.
- different than just "doing Agile", because Agile is too focused with features, whereas
  - The increments of development should be abstractions, not features.
  - Ideally, when you have finished with each change, the system will have the structure it would have had if you had designed it from the start with that change in mind.
- payoff for good design comes quickly. It's unlikely that tactical approach is faster even for the first version, let alone the second.
  - arguemnet against yagni
- The most important way to manage complexity is by shifting it from interfaces and into implementation:
  - Modules are interface and implementation.The best modules are where interface is much simpler than implementation.
  - It's more important for a module to have a simple interface than a simple implementation.
- An abstraction is a simplified view of an entity that omits unimportant details. Omitting details that are important leads to obscurity, creating a false abstraction.
- Each module should encapsulate a few pieces of knowledge, which represent design decisions. This knowledge should not appear in its interfaces,and hence are restricted to its implementation.Simpler interfaces correlate with better information hiding.
- The opposite of information hiding is information leakage:
  - When a design decision is used across multiple modules, coupling them together.
- Design it twice, taking radically different approaches.
- If you're not making the design better, you are probably making it worse.
