# Effective Software design

- [Effective Software design](#effective-software-design)
  * [What do you need to be effective?](#what-do-you-need-to-be-effective-)
  * [Context](#context)
  * [Change](#change)
  * [Complexity](#complexity)
  * [Evolution](#evolution)
  * [Guide](#guide)
  * [Links](#links)


- It’s not about principles, techniques or patterns.
- Being effective means that you are successful in producing a desired or intended result.
  - It means doing something that brings you closer to an intended goal. 
  - This implies that when you have done something with a certain outcome in mind, you should also be able to assess if you are any closer to that desired outcome.
- This implies that when you have done something with a certain outcome in mind, you should also be able to assess if you are any closer to that desired outcome.
- many developers just don’t know
  - They saw an opportunity for the pattern or design 
  - But did they really improve the code? Does the change have any impact on the desired outcome? Who knows.
  - **Did they think why it should be used, and evaluate if it was needed** 

## What do you need to be effective?

- you need to **know what software design is** and **what you want to get from it**
- software design is a process. 
  - it is an ongoing process
  - you continuously look for ways to structure the code solution in such a way that the future maintenance costs are kept as low as possible.
  - by enabling change in the solution and you do this every single time you have to touch the code.
- software design is a toolbox of best practices, patterns and techniques which can be used to enable change in code
- **is to understand**.
  - understanding of the most basic concepts in software design.
  - understand what it means to ‘enable change’.
    - any developer can relatively quickly find where change needs to happen in the code base 
    - the changes have a low chance of breaking the code or creating unwanted side effects
      - (for instance introducing bugs or the ripple effect where one change in the code ripples throughout the code base).
    - **change is isolated as much as possible. We should be able to predict which code parts need changing.** 
      - Because each module has a particular role, 
      - a particular function 
      - because these modules are isolated (as far as they can be totally isolated)
        - change will not spread uncontrollably
    - t will still cost a lot to maintain the code or the application. 
      - Because change will still spread. 
      - It will because you cannot have software modules that are completely isolated
  - **with every change you have to do, you need to make design decisions again and see if the result will still enable change while fulfilling the needs of the stakeholders.**
  - there is no best way to structure your code
    - depends on the domain you are working in and the stakeholders that are interested in the solution
    - depends on the current technology available

## Context

- Context defines your design 
- Depending on context, your design will be different 
- Changes in context, will change design 
- Context includes 
  - people (level, exp, knowledge, numbers)
  - tech (availability)
  - deadlines
  - economic/money
  - features
- The context you are working in is formed by the domain you are working in and what your stakeholders need and how they want it.
  - Your design should first of all meet the needs of the stakeholders
  - what stakeholders want or need is going to collide with your goal of enabling change. 
    - **where the needs of stakeholders and the goal of enabling change cross each other, that is where trade offs are born.**
  - Problem with coders
    - Believe that software designs principles, techniques and patterns are fundamental truths or dogma’s that need to be obied. 
      - It's not they are tools, and need to know when to use for the benefit of the stakeholder
    - Rather than it is the product produced that is the most important, what the users/stakeholders want
- **Software design it’s more what you’d call guidelines than actual rules**

## Change 

- change will always happen, if you can handle change then you will be left behind
- The main aim of software design is to enable to change, to make change easier
  - Has a cost - takes time, is hard to do, adds complexity
  - Trade off against other important design (ie maintainability, readability, performance etc)
- **We need to understand what the reasons are for change or where change is coming from.**
  - Otherwise, we won't know what form the change will take
  - which leads to how to design or implement this 
- **Problem with change, we dont know what will change, we cannot predict the future**
  - We can only have an educated guess (based on prior experience, statistics)
  - Only certainty is change will happen
  - If we design for the wrong change, can lead to wasted time, and hard to change places that really needed the change
  - The use of the **scientific method** is integral in software design
    - Allows to get fast feedback from experiments, to find out what is important, what does change often or slowly
- Where change comes from 
  - Stakeholders (majority of times) - new features, remove features, fixing bugs
  - regulation/security - regulations, laws, software updates, certificates 
  - internal - merging with recently acquired software bases, using newly procured services, top down initiatives 

## Complexity

- Has two sides 
  - the complexity of your solution
  - the complexity of the problem for which you are making a solution
    - Not talked about much
    - includes:
      - The complexity of the domain
      - the complexity of the stakeholders
        - More of them and especially if they have competing agendas, will lead to different variations
- in our interest to **keep the code solution simple, because we want to enable change.**

## Evolution

- due to constant change (the world, the tech, the people/stakeholders etc)
- This translates into more different needs and more possible variations. 
  - And your job is to build software that can still enable change with all of this in mind
- everything evolves and the complexity of the application evolves along. 
  - Evolution changes the context you work in.
- So  what seemed important in your design last year might possibly no longer be important and vice versa
- Your design must be able to handle constant change in an evolutionary style 
  - instead of doing a redesign (which has a lot of cost to it)

## Guide 
- There is no silver bullet, not dependent on techniques, patterns etc
  - These things are irrelavent and waste time discussing
- Follow this:
  - **You need to understand what software design is and what we want to accomplish with it. Understand what the goal is and also what it concretely means.**
  - **You need to understand context, to acknowledge it, recognize it and of course understand it. It is only by understanding the current context that you are able to make decent trade offs**
  - **You need to understand where change is coming from**
  - **You need to understand complexity and take it into account.**
  - **You need to understand the evolution of the context we work in.**
- AND START APPLYING IT

## Links 
- https://medium.com/@aboutcoding/the-importance-of-software-design-6acdc852e05f
- https://medium.com/@aboutcoding/best-way-to-learning-software-design-3a69c572f38a