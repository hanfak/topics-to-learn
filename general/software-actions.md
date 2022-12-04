# Software Actions

- As developers, we change software (including creating new Apps, deleting etc).
- Changing can make software easier or harder to change in the future
- Being able to change software, can be easier or harder depending on how it was written in the past

## Four reasons to change software

### Changing behaviour/functionality (Adding a feature &  Fixing a bug)

- The software behaves one way, and users say that the system needs to do something else
- Both are changing the behaviour of the software
- It's subjective to the users if the changing the behaviour is fixing a bug or adding feature
- To others it matters
  - As bugs and features are tracked, for quality or contractual reasons
- Behavior is the most important thing about software. It is what users depend on.
  - Users like it when we add behavior (provided it is what they really wanted),
  - but if we change or remove behavior they depend on (introduce bugs), they stop trusting us.
- Adding a method doesn’t change behavior unless the method is called somehow
- In agile thinking, both are the same, just feedback to improve the software to get closer to the end goal of the user

### Improving a design (Refactoring)
-  When we want to alter software’s structure to make it more maintainable, generally we want to keep its behavior intact also
  - if we lose previous behaviour then it is a bug
- People are scared of refactoring, but gain confidence if behaviour have a set of tests to prevent loss of behaviour
- Mainly changing structure of code

### Optimising resource usage
- Similar to refactoring
  - instead of program structure, we change how we use some resource ie time or memory

## Making risky changes

- Preserving existing behaviour despite adding new behaviour or fixing bugs or refactoring is a challenge
- To mitigate risk, we have to ask three questions:
  1. What changes do we have to make?
  2. How will we know that we’ve done them correctly?
  3. How will we know that we haven’t broken anything?
- How much change can you afford if changes are risky?
- How teams avoid risk in making changes
  -  They minimize the number of changes that they make to the code base
  - “If it’s not broke, don’t fix it.”
  - Just being cautious
- But this will still lead to problems
  - the existing ones grow larger and harder to understand.
  - When you make changes in any large system, you can expect to take a little time to get familiar with the area you are working with
- The difference between good systems and bad ones is that,
  - in the good ones, you feel pretty calm after you’ve done that learning, and you are confident in the change you are about to make.
    - You have a safety net -> tests
  - In poorly structured code, the move from figuring things out to making changes feels like jumping off a cliff to avoid a tiger. You hesitate and hesitate.
- Avoiding change has other bad consequences
  - Lose the skill
  - fear the code base
  - become slower at the change

## Reduce risk in making changes, having tests
- To avoid the issues above
  - **Have tests** or a safety net
- To avoid bad changes from leaking out
- We make some changes, run the tests to make sure nothing else has changed
- As part of making software, we need to have automated tests
