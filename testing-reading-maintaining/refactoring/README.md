# Refactoring

## What?

- To change the code but keep the behaviour the same.
- We can be certain behaviour is the same if we have test coverage of the behaviour
- Test coverage can be confident over the unit to be refactored, when applying TDD (or its flavours outside in, or inside out)

## Why?

- Reduce techincal debt
- Improve Non Functional aspects of the code ie maintainability, performance, extensibility etc
- Code written may be improved upon despite it doing what it is meant to do
- Reduce cost (time) to add features, reduce bug incidences, fix bugs, etc
- Reduces code rot which makes the codebase hard to work with, and can lead to devs leaving
- Does not mean complexity reduces completely, but can help
  - Longer an app is actively worked on the more features, bug fixes etc exist that increase complexity
  - Even non worked on apps can lead to complexity as it can be old, using old tech, no one knows the domain etc

## When to do?

- As part of TDD cycle
- When technical debt is too big and affecting current development on code base
- Refactor when changing parts for a current story, thus small refactors

## When to avoid?

- When time is tight, and the refactor is big and time consuming
- To avoid getting to perfection, focus on big wins
- When the app is beyond repair, and needs revamp
  - either due to new features or code rot

## Types of refactoring groups

- There are many refactoring methods (see Fowler) and these can be grouped (Fowler also groups them)
- Groups - there can be overlap
  - Technical Refactoring
    - Code is changed to improve it's ability to be extended, modified, testable etc
    - Lead to applying common software principles (SOLID etc) and design patterns (Gang of four etc). Leading to more abstractness
    - This can be small, but can be quite big (time and changing lots of code)
    - Updating dependencies or adding security patches
    - Issues
      - These changes may be more maintainable/extendable but can end up being less readable or navigatable for the develop to do the maintaince or add a feature.
        - abstractness is always more difficult to follow rather than concretness
      - This can lead to an explosion of files/classes/methods etc. Although IDEs makes this easy to navigate, understanding what is happening can be harder as logic is all spread out. Needs to be a balance.
  - Cognitive Refactoring
    - Make code more readable
    - Reduces cognitive load
      - Helps new joiners understand the code faster
      - Helps current devs who have not worked on code base for sometime
    - This can be architecture (package structure), keep all the main business logic in one or as few classes for each flow, domain driven design, better naming etc
    - Technical refactorings can also lead code to be more readable
    - Issues
      - Keeping logic in one place
      - Can lead to a lot of duplication
  - Style Refactoring
    - Codebases are generally worked upon by several developers. They need a shared standard to make it easier to work on the code.
    - This allows the code to follow the conventions in the codebase if similar work has already be done
    - For new projects, allows for decision to be easily made in it;s creation
    - Promotes good practice, what should be used and not
    - Makes it easier for everyone to follow the code, even non team members if the guide is used across temas
    - Use some style guide documentation
    - Issues
      - Can styling documentation may change for new projects, so different projects can be confusing
      - Older projects may not have it applied, but attempting to change can only be done in small doses
      - Needs to be constantly enforced (pairing/reviews/static analysis tests) otherwise individual developers will use their own styling which leads to a mish mash of styles
  - Reverse Refactoring
    - Can be temporary to help the developer understand the code. The changes are reversed before committing
    - Inlining, reordering, remove language constructs or syntatic sugar (lambdas -> annoymous classes)
      - can bring in code to make more sense
    - Reduces cognitive load to improve comprehension
  - Performance Refactoring
    - This can be app specific and also platform specific
    - Improve the performance of the app
      - reducing calls over the network or bottlenecks (ie services which has limit of being called)
      - Caching, object/connection pooling, concurrency/parallism, batching,
      - reducing time or space complexity
      - Fully tested (code coverage) for reliability
      - platform level (where the app is deployed) to improve scalability, availability, fault tolerence etc. But this may require changes to app to be able to use the platform, if you want your app to run
      - Use of static analysis (find bugs, sonar cube or custom tests etc) use common patterns which detect insecure code, vulnerabilities, test coverage etc. This informs the developer where refactorings can happen
    - Issues
      - Adding performance can be pre emptive, which leads to a lot of work done for little improvement.
        - Should test this, and see if it meets requirements
      - Doing it everywhere can lead to reduced maintainability and readability, thus changes will take longer
        - should be done to the main culprits and encapsulated
      - Due to complexity, more comments and documentation will be needed, alot more complex testing too
  - Documentation Refactoring
    - Additons and/or changes to comments, documentation files, diagrams etc
    - When the above refactorings happens or bugs/new features documentation maybe out of date and need to be improved
    - Useful for new joiners
    - Issuse
      - Can go out of date very quickly
        - Can use html rendered acceptance test (yatpsec, cucumber etc) which turn tests into readable documents. Helps for business documentation, but not for technical side of the app
        - Time constraints leads to ignoring updating comments
      - Can be a duplication of effort
        - use of wrong comments (how rathe than why answered in comments)
        - Have code cognitively refactored should reduce the need for majority of comments, as code is the document
      - Adds too much noise
      - Time taken may not be worth it

## ROI of refactoring

- https://neilonsoftware.com/talks/the-roi-of-refactoring-lego-vs-play-doh/

## Premature refactoring

- Many articles about TDD emphasize the refactoring step - as in the green step is almost trivial/unimportant, and what really matters is the refactoring step. Developers misinterpret this as having to get to some over-engineered design at the start. 

An example of a misconception: "if-else" isn't clean - so let's use polymorphism everywhere; we must remove all if-else statements during refactoring. The other reason (in the developer's mind) is an expectation of future requirements; the developer assumes certain requirements in the future and thus makes their CURRENT code MORE ABSTRACT to fit the predicted FUTURE needs.

The problem with premature refactoring:

1. The developer must now spend more time considering the more complex solution. This is actually wasted time.

2. The unnecessarily more complex solution means higher maintenance costs in the future. Again, wasted time.

3. When the future comes, and we get user feedback, it turns out that the real needs are different compared to what we had predicted now... So then the current abstraction has to be deleted (wasted effort) and implement the right abstraction.

So what's the solution? Deferred refactoring:

1. During the refactoring step, it's ok to do minor refactoring, such as variable renaming. But let's not get into the trap of trying to refactor the if-else into a polymorphic solution and trying to apply design patterns right now!

2. Since we have a simpler solution (the simplest solution that was enough to solve the problem), we don't have unnecessary maintenance overhead.

3. The future will come - when it comes. A month from now, it might turn out that the if-else statement is still working great. Three months pass, and the if-else statement is still working fine. After six months, due to some new requirements, and our better understanding of the business problem, we realize that we could replace the if-else statement with design pattern XYZ; at that point, "it feels right".
