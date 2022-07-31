# 2. Open Close Principle

- a class should be open for extension, but closed for modification.
- it should be possible to add or change some behaviour without modifying the existing class
- Good architecture maximizes the number of decisions not made
- You should be able to change a component's behavior w/o modifying the componen
-  Any time we create code with the intent to extend it in the future without the need to modify it we should apply OCP
- 3 strike rule
  - if having to do this samething three times, abstract it out

## Why?

- If existing code is not being changed, but rather extended to account for new requirement, the fear of changing it is lower and the number of costly defects may be reduced.
- allows us to leave more options available and delay decisions about the details
- reduces the need to change existing code
- to increase flexibility of your software and make future changes cheaper
-  By allowing parts of the solution to change independently, you reduce the scope of changes necessary

## Issues

- So the open-closed principle states you should not modify existing behaviour. And what if there's a bug in it? What do you do?
  - Fix it in code thus breaking closed for modifying
  - use inheritance, subclass it, and use new object, but that leaves the original object available and bug still exists
  - Use decorator, but bug still exists
  - Maybe this issue does not apply to classes but bigger sizes (libraries/http api etc)
    - Meyer was talking about this ( Object-Oriented Software Construction
- There is a school of thought, that if there is a bug, then the code was never complete, so it is ok to modify
  - As requirements change all the time (ie need for agile) then code is never in a finished state so modifying the code should be fine
- Adding un-needed flexibility to code (to make it open for extension) breeds complexity and carrying cost.
  - It requires imagining all sorts of use-cases that don’t exist in order to make it ultimately flexible. This wastes time, creates more complex and complicated code, and requires that you maintain, in perpetuity, all this flexibility that you don’t need.
- The idea you cannot change the code, is ludacris
- Highly flexible code creates a lot of code paths to navigate, and the type of flexibility demonstrated in the paper—added abstract base classes—makes those code paths hard to discover.
- You cannot predict what will change, you have to have a good guess or know future requirements and make them dependencies to inject in or some other pattern to abstract out code that changes
  - you could go all the way and make everything abstracted out, so that any changes can be handled, but the code then becomes hard to understand, complex, logic spread out etc
  - To handle this, you can make the change in the code, and decide if this change needs to be abstracted or not
    - Can look at git history to see if this logic has been change regularly
    - YAGNI
- Using class inheritance (Extends) might be used to implement this idea
  -  Inheritance should be used in “X is a type of Y” relationships and not just as a behavior expansion mechanism. If so, we end up with an extensive genealogy of classes, which is even more rigid and problematic


### Links
- https://www.quora.com/A-tech-interviewer-once-got-me-stuck-with-a-question-So-the-open-closed-principle-states-you-should-not-modify-existing-behavior-And-what-if-theres-a-bug-in-it-You-dont-fix-it-How-was-I-supposed-to-answer-this
- https://naildrivin5.com/blog/2019/11/14/open-closed-principle-is-confusing-and-well-wrong.html

## Links

- https://stackify.com/solid-design-open-closed-principle/
- https://dzone.com/articles/solid-principles-openclosed-principle
