# Working with legacy code

What?

- “source code that relates to a no-longer supported or manufactured operating system or other computer technology.”
-  legacy code as code without tests
- legacy code the code that was written before they arrived in a company.
- code that:
  1) is hard for you to understand,
  2) you’re not comfortable changing,
  3) and you’re somehow concerned with.

- Legacy help the code grow
- Without legacy code, you would not have a job
- People wrote legacy code without realising it would be legacy code
  - Best practices change
  - Technology has changes ie language features and hardware
  - What was required then for outcome of codebase has changed
  - There were other constraints, time, business, money

- There can be parts of codebase which is legacy

- If there are no tests around a piece of code, you won’t be comfortable changing it.
  - very cautious when you add a feature, because it could have an impact on this existing code.
  - have to spend time writing tests, maybe even refactor existing code in order to write tests, deal with regressions

- need to understand someone else’s writing, or plenty of people’s writings combined
  - think about why they did what they did.
  - understand the structures in the code and how they relate together.
  - Legacy code becomes tangled and difficult to understand because of an inconsistent accumulation of changes, made by many people, who sometimes weren’t even employed by the company at the same time.

## How to approach legacy code

### Attitude

- you’re paid for being rational, not for being primal
- the best code we can write now might be laughed at in ten years
- When view code, think
  - had I been given the chance, would I have done so much better at that time?
- Take ownership
  - don’t complain if you are not intending to improve the code.
  -  consider that the code you’re working on is your code.
  - acknowledging that you are the one in charge now of the code
- Have role model
  - With right mindset
- Learning from bad code
  - in legacy, what you learn tends to be specific knowledge about how the codebase is organized, rather than how to get better at development
- not improving your skills is dangerous in the long term
- you still can (and should) evaluate objectively the quality of your code and code you work with
  - explain why you don’t like it.
  - What’s wrong with that particular piece of code?
  - If you don’t like it, there must be something wrong with it, right?
  - If it’s just a matter of style, then don’t dwell on it
  - be precise
- becoming more familiar with the code, seeing how code is structured and, most importantly: learning what to pay attention to.
- to explain it to other people
- think about why the code is now better than before you changed it.
  - elaborate
  - Have a good reason why
- Workign wiht bad code, helps you find it again and solve it in other places
- Work with and read good code
  - a lot of what writing good code is about comes down to making proper use of abstraction levels, and deciding which abstractions to put in place is the first step to a good design.
  - design issues stand out to you with more accuracy when reading bad code
  - Where is good code
    - standard library of language
      - Documentation
      - implementation
      - read the code that uses it
    - Popular and mature external libraries
    - Open source projects

## Understand Legacy code

### Get an overivew of code

- Stronghold in the code
  - to pick a place in the code that you understand very well (or at least, better than the rest of the code).
    - ie inputs and outputs of that feature in the application
  - Starting point to build your map of the code, the directions to other code
  - Can use a dubugger from there
  - a small unit or line of code that you understand perfectly in the context of the application.
  - Once you have that reduced scope of where to look in codebase, explore it by reading the code or stepping through it with a debugger.
  - focus on cues that look related to the unit you’re after, until you step through to the area you were looking for
  - needs to be specific.
    - A commonly used method is not useful
    -  some business code that calls this function in a context that you know in the application is a better stronghold.
  - Find someone with some experience of the code, to give you starting point for a strong hold
- Starting from the inputs and outputs of the program
  - If no one has worked in the code,  find some one who has used the code ie it's interfaces
    - Ask for a common use case, how they interact with the app ie gui/postman etc
  - If no, look at integration tests
    - look documentation for how libraries are implemented ie to start a server and accept requests etc
  - Code must take some input, find this
    - use grep
  - Once you have found a trace of the UI input or output in the code, ollow it like a thread until you reach the code of the test case that the business person showed you
    - To work from UI layer to business layer, need to understand UI framework
    - study how information is carried from graphical events to business code and back
- Analysing code stacks
  - to fire up the debugger, find a “judicious” place in the code where to put a breakpoint, and launch a use case in the application.
    - A judicious breakpoint is one that is deep in a stack of a typical use case of the application.
  - the call stack displays in one shot all the layers of the application involved in that use case.
    - this snapshot provides insights on the architecture of your software: what the main modules and the frameworks are and how they relate together.
  - Repeat this experiment for several call stacks in the same use case in order to get a grasp of the sequencing of the calls
    - And for other use cases
  - Flame graphs
    - They aggregate the data produced by a performance analysis tool (such as perf on Linux) into a picture representing the stacks that a program went through during its execution.
    - Display several call stacks at the same time

### Reading code faster

- Speed reading
  - Code is non fiction
  - An inspectional reading consists in skimming through the book, looking for places that sum up the information (table of contents, beginning and end of chapters, main messages...).
  - This skimming of the code allows to achieve two things:
    - deciding whether this piece of code is relevant for you and deserves a deeper analysis,
    - getting a general idea of its meaning before getting into the details.
  - you do not want to start by reading a function “cover to cover”,
  - only when you have performed the inspectional reading should you read the code in more detail
    - Only code that is important, thus reducing code to read
- Working your way backwards from the function’s outputs
  - Check the function name first
    - should be well named
    - the name, parameters and return type should be enough to indicate everything you need to know about this function.
    - If function signature is poor, look inside
      - check outputs first,
        - For one return, general last line
        - For multiple return statements
          - find commonality between them all
        - For void methods
          - doing side effects
          - check modifying their parameters or, for object methods, modi- fying the state of the object.
        - Modifying global variables
        - Throwing exceptions
- Identifying the terms that occur frequently
  - Use a word count frequency tool in function/class
  - look for the objects that appear the most frequently in its code.
    - More frequent, the more central it is to function
  - Highlight them using IDE
  - If object is spread out through out thr function, it is important
  - Understanding how inputs are used
    - examine what it does with its inputs.
    - If used at beginning, to get another object then these might be more useful to follow
  - is the intensive use of a word in a portion of the code, and very few usages outside of this portion
    - his portion of code is focused on using a particular object, which can clarify the responsibilities of the portion of code
- Filtering on control flow
  - instantly squeeze a long the function into a few lines of code is to filter on its control flow keywords: if, else, for, while, switch, case, try, catch
    - hide all the lines of the function except those that contain the control flow keywords
    - shows the skeleton of the function, ie table of contents
- Distinguishing the main action of the function
  - in a function, not all lines contain the main action
  - Some lines are merely secondary quests, like getting a value, logging a piece of information, or preparing a secondary character.
    - Should not focus on
  - To locate the main action, you can quickly scan every line of the function, and determine if it looks like the main action, even if with a gut feeling.
    - Dont spend too long on this
  - achieving a 100% understanding of a long function the first time you encounter it is not always a good objective.
    - Comes wiht cost of time
    - And may not need full understanding to change or add feature
    - When to spend time understanding
      - they can be functions that have a bug in a corner case and that you need to fix, functions that you choose to refactor, or high level functions that show the structure of an important feature of the application

### Understand code in detail

- Using “practice” functions to improve your code-reading skills
  - A “practice” function is a big function that has a complex implementation but that has little to no dependency on anything else
    - It is self contained
  - get familiar with code, style, not always a good standard of quality
- Decoupling the code
  - Start refactoring code
    - That changes structure of code, or puts in a structure
    - Decoupling entities
  - break down function into sub functions
    - To keep only the control flow in the original function and factor out each sub step or special case in its own separate well-named functions
  - decouple data processing from objects
  - Refactoring is high time intensive activity
    - Need to see what gives most bang for the buck
- Work with others
  - working on your own to understand code you know little will take longer than working with someone who does or more experience.
    - Pair programming
  - Use of a rubber duck
  - Just explaining it can also help

## Knowledge

### Knowledge is Power

### How to make knowledge flow in your team

### The Dailies

## Cutting through legacy code

### How to find the source of a bug without knowing a lot of code

- Maintaince is associated with using a debugger to find the error/bug in code
- The natural way of find bug (inefficient):
  - 1. You receive a bug report related feature X
  - 2. You look around the code of feature X
  - 3. You step through the codebase with the debugger, looking for the cause of the problem.
  -  if you start by looking at the code, you don’t know what you’re looking for
    - Stumble into bug
- don’t start by looking at the code.
  - **begin by spending time analysing the application while it is running.**
- Better approach
  - Step 0: Dont look at code
  - Step 1: Reproduce the issue
    - Check the bug is there
    - Check bug is in on dev machine
      - if not then could be environment specific, config etc
  - Step 2: Perform differential testing to locate the issue
    - After reproducing bug
    - Reduce the test case
      - trying slight variations of the original test case in order to refine the scope of the bug
      - Aim of finding simplest test case to reproduce bug
    - Step 2a: Start with a tiny difference
      - Change something small between two configs, then the delta is where the issue is
    - Step 2b: Continue with larger differences
      - Maybe differences between new feature and old version
  - Step 3: Formulate and validate a hypothesis
    - After we end up with a probable location for the bug and a method for reliably reproducing it
    - We formulate a hypothesis about what is causing the incorrect behaviour.
      - If many things go wrong choose gut feeling
    - Now look at code to confirm it, use debugger here
    - If validates hypothesis, great, if not repeat this step
  - Binary search for root cause of bug
    - Use divide and conquer, to quickly get to a bug
    - narrowing the search by repeatedly splitting up the search space into a good half and a bad half, then looking further into the bad half for the problem.


### What to fix and not fix

- Can be like a bully
  - Big code base, inconsistent, duplicates, big functions/objects
  - When fixed, a regression test fails
  - Need a strategy to help fix code
- The value-based approach
  - Problem is there are many areas to fix, but little time
  - Do lots of refactoring or rewrite is not feasible
  - Need to assess both the value and the cost, for each refactoring that you are considering.
    - act on the best value/cost ratios
  - Sources of costs to think about
    - Changing prod code
    - fixing regressions
    - adding tests
    - handling conflicts
  - There will be unknown unknowns that will add to the costs
  - To refactor, need to understand code -> takes time
  - The cost of the regression depends on two things:
    - how long it takes to identify what caused the regression - how long it takes to fix it.
    - Both those amounts of time are correlated with how close your tests are to the code.
    - The farther a test is from the code, the longer it takes to launch and the less often it’s launched
    - Use of unit tests, that run often, reduces fixes time, and increase fix is done correctly
    - The test that is the farthest from the code is when a client uses the software
      - Regressions discovered by a user are amongst the longest to identify and fix.
      - Due to context switching, bad rep, new release, research etc
  - Adding tests
    - time needed to write tests includes thinking of the scenarios to test and implementing them
    - Most of the time taken in writing tests is doing that one last thing to cut off a dependency so that the code under test can be put into a test harness.
      - refactoring code to make it more testable
  - Handling conflicts
    - good candidates for refactoring are regions of code that get in your way
    - Hot spots are areas of code where lots of current dev work is occuring.
      - can lead to merge conflicts
      - identify hot spots is to look in your version control system what parts of the code tend to be modified very often, and to understand why they need more fixes than the rest of the code
      - Other potential hot spots are those that come up in bug reports on a regular basis, as well as those where a lot of regressions appear.
    - Refactoring hotspots takes coordination between devs
    - Try having only one developer at a time is allowed to work on a refactoring on a hot spot.
      - developers aren’t allowed to exceed one or two days of lock time
  - every developer of the team marks off places in the code every time something related to the quality of the code slowed them down, while debugging or fixing a bug, or in any other development activity
- Valuable refactorings
  - What annoys you the most in your codebase on a daily basis?
  - Get team invovled in deciding
  - Slice up a big function
    - Forces devs to be bog down into details and not get a big picture of what is going on quickly
    - Identifying the responsibilities of that function to split into sub functions with good naming
      - Or delegate to another object
    - If function is used a lot, then prime candidate
  - Slice up a big object
    - Object might have lots of responsibilities
    - Splitting their members allows you to manipulate lighter structures that take up less mental space in the mind of a reader.
  - Make side effects visible
    - Making it clear what effects a function has on objects helps following along and being less surprised when debugging code.
    - use of built in language features to make immutable objects
    - you can pass in the objects to be modified as function argument instead of global variable
    - bundle the function that makes a side effect on a piece of data with it into a class
    - make it clear in a function’s name what side effects it has
  - Use names that make sense
    - Poorly named objects can send you on a wrong track and make you waste a lot of time.
  - Don’t Repeat Yourself
    - Two (or more) identical pieces of code in the codebase means
      - more code to become familiar with
      - more places for bugs to settle in
      - more intellectual strain to fit everything in your head
    - duplicated code that start off as identical tend to evolve in separate directions
    - Merging two exact duplicates, that haven’t had the time to diverge yet.
      - preventing diverging
    - Merging two non-identical duplicates, that have already diverged.
      - harder, need to find commanlity
      - a first step is to place them next to each other in code
- talking about the code in terms of the target design, even before you carry out a refactoring project

### refactoring techniques to reduce function size

- long functions/classes make legacy code hard to work with
  - Also over engineered (lots of patterns/abstractions)
