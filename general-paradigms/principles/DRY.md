# Dont Repeat Yourself

- Repeating yourself, means wasting time, time that could be used to do other stuff
- DRY is about wasting time
- **Focus on not repeating the business logic, this is should be one place**
- Areas of wasting time
  - Following an inefficient process
    - This can occur in the release cycle, the way new features are designed, sign-offs, or meetings
      - Use feedback, retros, to find out the waste and improve processes
      - automate these processes
    - Hearing we have alwasy done it, is a sign of inefficiency
  - Lack of automation
    - ie
      - deploying manually
      - compiling
      - testing
      - building
      - configuring development machines
      - provisioning servers
      - documenting APIs
    - Try to automate your builds and deployments from day one, as they will only get more complicated as you go along
  - Not invented here, also known as reinventing the wheel
    - arising from writing code before considering the reuse of existing code
    - people who enjoy implementing things that are easily available (inhouse or in open-source world)
    - Always search for libraries which do what you want
      - but make sure it can do exactly what you need, and if not it can be configured, do spikes
  - Copy/paste programming - this is a common misconception of DRY addressed by the authors of it
    - Leads to errors
    - Leads to multiple places where changes need to occur
  - “I won’t need it again so let’s just hack it quickly” solutions
    - Never good if not tested
- Not doing so means changing in one place, means having to remember to change in other places
- Copy and Paste Programming
  - the more code you write, the more expensive it becomes to support and maintain the application
  - Both composition and inheritance are your friends in battling repetitive code
  - the use of design patterns and shared libraries.
  - web services to combat duplication on higher levels of abstraction.
    - Instead of building the same functionality into each application you develop, it is often a good idea to create a service and reuse it across the company.

## Examples 

- Libraries 
  - but can lead to coupling

## When to use

- Better to do it after it is apparent 
  - Not extract when no duplication occurs in the hopes of reusue
  - Three occurrences and then dry 
  - If it is known that the future requirements will be similar than dry
- When it is regarding source of knowledge, not just patterns 
- Benefits outweigh the negatives, especially the time investment
- It follows the idea of ETC (easier to change), it makes it:
  - easier to read
  - faster to extend or change

## Acid Test

- the acid test: when some single facet of the code has to change, do you find yourself making that change in multiple places, and in multiple different formats? Do you have to change code and documentation, or a database schema and a structure that holds it, or…?
- Best to time box the drying up of code, and see if it improves the codebase (ie ETC), and revert if not

## Types

- Imposed duplication.
  - Developers feel they have no choice
  - the environment seems to require duplication.
- Inadvertent duplication.
  - Developers don’t realize that they are duplicating information.
- Impatient duplication.
  - Developers get lazy and duplicate because it seems easier.
- Interdeveloper duplication.
  - Multiple people on a team (or on different teams) duplicate a piece of information

## Pitfulls and issues

- A little duplication is often better than a little dependency.
- Prematurely optimize when the requirements aren't finalized (spoiler: they never are).
  - Hence, the abstraction may need to change to cater for different cases for different consumer needs
  - https://overreacted.io/goodbye-clean-code/
  - https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction
- Duplication is a convenient but not the best source for discovering abstractions
- wrong abstraction at a lower level creates an exponentially worse dependency hell at higher levels.
- There is always a trade off
  - sometimes better to copy and paste, and minimal changes, instead of having lots of logic
  - Time to refactor might be too long to remove duplication, and changing other code will require retesting
  - To much dry code can result in complex code, too much abstraction and hard to understand
- **Removing Duplication Requires Abstractions and Abstractions Breed Complexity**
  - Such generalized abstractions are notoriously hard to test and understand because they must handle many more use-cases than the original (potentially duplicated) code.
  - Said another way, abstractions support more behaviors than might actually be needed for the system to function properly.
  - Thus, the removal of duplication can introduce new behaviors to the system that aren’t required.
  - Duplicated code tends to also obscure the structure and intent of your code, making it harder to understand and modify
  - If an abstraction exists, then future change will feel the need to use this abstraction ( and thus change it) which leads to pollution of ideas and complexity
- This was first promoted in Pragmatic Programmer (Thomas)
  - In the second edition, they realised that it was not the correct message, as people took it too far
    - people believe that no copy and pasting was allowed
  - Instead Duplication of business logic should not be repeated, there should be a single source of truth
    - 
  - DRY is about the duplication of knowledge, of intent. It’s about expressing the same thing in two different places, possibly in two totally different ways
  - Dont dry coincidental duplication only essential duplication 
    - essential duplication are parts that should change together 
- When a duplication is abstracted, and changes are needed for only on consumer of this abstraction, this can lead to clauses (if statements) proliferating the code base
  - instead duplicate the code 
- Lead to tight coupling
  - prefer some duplication instead
- DRY can make it harder to debug 
  - Should think very carefully to do this in test code otherwise can be hard to follow intent or debug
- For small amount of duplication is not worth it

### Links

- https://www.infoq.com/news/2012/05/DRY-code-duplication-coupling/
- https://oncodedesign.com/dry-vs-coupling/
- https://www.industriallogic.com/blog/spot-and-coincidental-duplication/
- https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction
- https://www.entropywins.wtf/blog/2017/09/06/the-fallacy-of-dry/
- https://rotemtam.com/2020/05/18/the-dry-principle-is-bad-advice/
- https://gordonc.bearblog.dev/dry-most-over-rated-programming-principle/
- https://salmonmode.github.io/2020/08/14/the-harmful-obsession-with-dry.html

### Issues with many small methods

- Implementing DRY can lead to creating many methods, and the use of the popular refactoring Extract Method.
- Sometimes it is better to fold the mehtods in (Inline Method)
- writing functions that are nothing but 50 functions calls that themselves are just a few lines of code. That's as bad as the people who write 1,000 line functions
- This can cause issues:
  - Lots of little methods makes code get hard to maintain
  - costs to breaking code up:
    - more cognitive load when a reader must jump around a file and remember what different functions do
      - Logic is split apart and harder to follow
    - too many functions means more lines of code that makes it harder to see more of the code on your screen at once
    - more functions means more argument and return value passing which increases the chance for bugs
    - separating two very related pieces of functionality (get next free id and update next free id) increases the chance for bugs when someone updates one piece of the functionality and doesn't realize they need to update other related functionality in a different function.
      - issue of temporal coupling, calls need to be together if they are dependent in order
    - pulling more functions out makes it more likely that someone will reuse that function for something else which builds up complex dependencies making it harder to change some of the code because you have to understand much more of the codebase to safely change the code.
    -
- https://www.reddit.com/r/ExperiencedDevs/comments/u7xynw/many_small_methods_make_code_hard_to_maintain/

### Keeping long blocks of code managable

- long blocks of code (within reason) are made much easier to consume when they are broken up and commented well. I approach it but looking at the logic flow, then separate lines and blocks of code that are discrete logical steps in that flow, comment each, and only THEN ask myself what would make it better as another functio
