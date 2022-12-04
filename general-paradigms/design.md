# Design

-  design is there to enable you to keep changing the software easily in the long term.
  - Software change curve, states that changes later in the project/process(SDLC) is exponentially more expensive
- As design deteriorates, so does your ability to make changes effectively. -> software entropy
  - Bugs breed faster, and harder to fix,
  - Features harder to add
  - Changes  become exponentially expensive

## Issues

- Since XP/Agile, there is a movement that has led to software to be created without any design to avoid any design upfront, and just code and use refactoring to let the design emerge.
  - This was in response to waterfall, where everything was designed before any coding (Big up front desing - BUFD), which tried to predict everything which was impossible
  - fundamental assumption underlying XP is that it is possible to flatten the change curve enough to make evolutionary design work.
- But Agile is about shortening the feedback loop, so it's like lots of mini cycles of waterfall in short iterations, to get a product out to the users for fast feedback
  - This means there should be some design, but not a whole lot
- Needs to have mix of both ideas
- This has led to styles
  - Evolutionary and Planned Design

## Planned Design

- Borrows from engineering field
- Follows:
  - Designers think out the big issues in advance.
    - They don't need to write code because they aren't building the software, they are designing it.
    - they can use a design technique like the UML that gets away from some of the details of programming and allows the designers to work at a more abstract level.
  - Once the design is done they can hand it off to a separate group (or even a separate company) to build.
    - Since the designers are thinking on a larger scale, they can avoid the series of tactical decisions that lead to software entropy.
  - The programmers can follow the direction of the design and, providing they follow the design, have a well built system

### Issues

-  Changing requirements are the number one big issue
  - A design can be planned to deal with areas of volatility, but while that will help for foreseen requirements changes, it won't help (and can hurt) for unforeseen changes.
  - It is hard to know what are the volatile areas to design for
  -  Designers cannot rely on requirements provided to be correct or not changing
-  it's impossible to think through all the issues that you need to deal with when you are programming.
  -  when programming you will find things that question the design. However if the designers are done, moved onto another project, what happens? The programmers start coding around the design and entropy sets in
  - it takes time to sort out the design issues, change the drawings, and then alter the code
- Designers are not programmers anymore, and end up losing their technical skills and appreciation for coding, stuck in a time warp
  - Thus coders lose respect and belief in the designers, and vice versa
- any programmer working in high design environments needs to be very skilled. Skilled enough to question the designer's designs
  - Otherwise, code will be done with question and could end up being not what was intended
- planned design dominates because the assumption is that you can't change your mind later.


## Evolutionary Design

-  the design of the system grows as the system is implemented. Design is part of the programming processes and as the program evolves the design changes.
- But this idea, ends up being the aggregation of a bunch of ad-hoc tactical decisions, each of which makes the code harder to alter.
  - in essence no design

### Issues

- It is like hacking
- Entropy can hit faster
- Issues which could have been found earlier and mitigated, are part of the system
- Different styles of design can evolve
- For complex systems this can lead to fast start but severe issues later
- Adhoc designs or designs just in time, can miss the big picture, which leads to possible rewrites of huge areas of the code base, or even rewriting the system, to cater for miss areas


## XP - Better way?

- By flattening the software change curve, can allow for evolutionary design
  - But this requires testing, refactoring (TDD) and CI
  -  As the cost of change lowers then you can do more of your design later as refactoring
- Planned design does not go away
  - Can happen before any coding, or before the iterations
- Use of YAGNI
  - The issue comes with such things as frameworks, reusable components, and flexible design.
    - complicated to build
    - pay an extra up-front cost to build them, in the expectation that you will gain back that cost later
- XP's advice is that you not build flexible components and frameworks for the first case that needs that functionality
  - Why
    - Economic - time, effort and money saved
    - Not providing what the customer wants
    - As this was not required, and no detailed requirements about it, we are likely to get it wrong
    -  a complex design is more difficult to understand than a simple design. Therefore any modification of the system is made harder by added complexity. Increases cost of modification
      - This leads to being fixed to this complex design, or
      - changing the design cause it was wrong
### What about design patterns
  - In general, pattern usage is overused and not used for the right reasons
    - effective design argues that we need to know the price of a pattern is worth paying
    - but patterns are a backbone of design knowledge,
  - the idea that simple desing and refactoring will lead you to design patterns
    -  Surely it's better if you know roughly where you're going and have a book that can help you through the issues instead of having to invent it all yourself.
  -  XP emphasizes both not using a pattern until it's needed and evolving your way into a pattern via a simple implementation.
  - If refactoring leads to a pattern, try it out, but dont be afraid to revert it if the benefits are not worth it

### Architecture

-  architecture conveys a notion of the core elements of the system, the pieces that are difficult to change. A foundation on which the rest must be built.
- XPs critics state that XP ignores architecture, that XP's route is to go to code fast and trust that refactoring that will solve all design issues.
  - which is a weakness
  - Have your systems decoupled from the architectural decisions
- there is a role for a broad starting point architecture
  - ie
    -  stating early on how to layer the application
    - how you'll interact with the database (if you need one)
    - what approach to use to handle the web server
  - these early architectural decisions aren't expected to be set in stone, or rather the team knows that they may err in their early decisions, and should have the courage to fix them.   

## Links

- https://www.martinfowler.com/articles/designDead.html
