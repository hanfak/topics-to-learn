# Simple and Easy

- We generally want simple software and focus on this, but we also want easy software which is less focused on
- Simple → Complex 
  - is the dimension that describes how irregular and interconnected a system is. 
  - Simple systems can be broken down into smaller pieces that are understandable in isolation. 
  - If you make changes to one of those pieces, you don’t have to fear unexpected ramifications in parts not directly connected to what you’re operating on. 
  - Complex systems are the exact opposite: you’ll need to keep in mind a lot of things and tread carefully.
- Easy → Hard 
  - is the dimension of how much energy and time it takes to successfully execute something. 
  - Easy things generally require less preparation and can be done reliably even by inexperienced individuals.
  - hard stuff requires more effort and not everybody gets it right all the time.
- complex things tend to be hard, while simple things tend to be easy
  - But this can shift very quickly

## Building Abstraction 
- Every time you build an abstraction, you encapsulate a given amount of complexity, making it easier to use
  - abstraction makes it easy to use, but the complexity is hidden
- Abstraction does not get rid of complexity or decrease it
- abstraction is a step towards composing bigger systems without increasing complexity too much
- With out abstraction, we would need to rewrite and write a lot to do stuff, this will lead to slow building of things and make things less economically viable
  - This is why we don’t write everything in assembly
  - Using higher level languages abstracts the assembly level language, but does not get rid of the complexity
  -  none of these things further simplifies assembly code, but they do actively prevent it from exploding in terms of complexity
- NOT ALL ABSTRACTION MANAGES COMPLEXITY
  - Abstraction is sometimes introduced just to make things easier. 
  - ie introducing a new interface with the sole goal of making it easier to swap in and out a replacement for a componen
- EASY IS BETTER THAN HARD
  - no reason to prefer hard over easy
  - The cheaper we can do it for, the more we can have, and the benefits compound over time
- THE RULES OF ABSTRACTION
  - introducing abstraction has two main effects
    - Lowers difficulty by hiding some of the details. Fewer lines to write, fewer things to keep in mind and think about — or even to right out know.
    - Identifies a cohesive subsystem and draws a box around it. The box becomes then a tool that can be reused to build bigger systems, while keeping complexity down.
- complexity management, is not trivial. It’s easier to lower difficulty rather than constrain complexity
  - easy software that encapsulates more complexity than it should.

## Easy complexity
- Causes all kinds of problems
  - called bloat
  - describing something that fails to manage complexity in a misguided effort to make things easy.
- USING BLOATED TOOLS
  - being resource-hungry and needlessly slow.
  - Developers that over-rely on this type of tool get progressively caught in a form of lock-in where the tool removes them from the details of what they are doing (“the tool does it for me”), making them more productive, but at an unfair price
  - when you only approximately know one way of doing things, you will also be limited in the range of things you can do
  - This leads to finding fixes and hacks to make the tool work for the problem 
    - Some will give up on the tool, after failures
    - Others will continue, but be affected with new releases that breaks their solution
  - choosing slow and unreliable tools will make you a slow, unreliable developer with a limited and quickly depreciating skill set.
  -  when you can understand what you’re doing, troubleshoot problems, and in general be able to iterate quickly, then you will have a real opportunity for improvement.
- NOT ALL BLOAT IS EVIL
  -  the biggest number of that type of developers comes from different ecosystems where bloat is the result of hostile design

- A reliable environment is a fundamental prerequisite for building competence.
-  important prerequisite is a feedback loop that allows you to quickly gauge the result of your actions.
- Using bloated frameworks will prevent you from understanding the details of what you’re doing and cause your software to inherit bad traits such as slowness and unreliability, 
-  It doesn’t matter how easy you try to make things: complexity is an almost radioactive source of difficulty.
- Focus on value over time
