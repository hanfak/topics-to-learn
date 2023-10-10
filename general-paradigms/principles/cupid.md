# CUPID

- An alternative to SOLID
- Focus on properties rather than principles 
  - Principles are like rules: you are either compliant or you are not. This gives rise to “bounded sets” of rule-followers and rule-enforcers
  - Where as properties
    - rely on qualities or characteristics of code rather than rules to follow.
    - define a goal or centre to move towards

Definitions:

## Composable: plays well with others

  - Code that is easy to use, gets used, used and reused
  - pipes in unix

### Small surface area

- less to learn
- less to go wrong
- Less to conflict
- Less inconsistency with other code you are using
- Goldilocks just right, to getting it right between too fragmented and bloated
- Issue
  - Has diminishing return
  - ie if your APIs are too narrow, you find yourself using groups of them together, and knowing “the right combination” for common use cases becomes tacit knowledge that can be a barrier to entry.
- For example 
  - narrow, opinionated API
  
### Intention revealing name and purpose

  - easy to discover
  - easy to evaluate 
    - to use it, or find something else, or adapt it
  - Knows what it does with out looking at internals
  - ie Having different levels of documentations or video tutorials (varying lengths, depths etc) that allows user to assess and get out when needs met

### minimal dependencies

  - Avoid the whole wanted a banana but got a gorilla holding the banana ie node
  - Avoid adding dependencies which could conflict transitively with clients
    - ie version or library incompatibilities
    - ie avoid adding libraries in your libraries that will may conflict with the users of it
  - Less to worry about

### Reviewing code

  - Does the class/method/function have any dependencies that aren't strictly necessary? If so, how can we remove them, or externalise them and make them optional?
  - Does the code have a small, opinionated interface or API? If not, how can we reduce its surface area?

## Unix philosophy: does one thing well

  - Unix is one of the successful software, with a philosophy behind how it should do things 
    - A lot of the cupid ideas stem from this philosophy
  - Have a consistent and simple model
    - predictable
  - Have components that work well together 
    - composable 
  - Functional paradigm
  - Make each program do one thing well and only one thing
    - "ls" list  flie details, but no inspection of files
  - Together with composability there is nothing you cannot do
    - Expect the output of every program/method to become the input to another
    - pipes , streams api
  - Different to SRP
    - about what code does instead of how the code changes
    - The organsiation of code
    - inside out
    - Focus on having one reason to change, can lead to artificial seam 
  - Instead of SRP do Single Purpose 
    - Doing one thing well
    - outside in
    - 
  - Reviewing code
    - Does each part of the code do one and only one thing, and is it obvious what it doesn't do, and what the edge cases are? If it is doing too much, can we see where to introduce a seam and break things up?
    
## Predictable: does what you expect

  - Should be consistent, reliable, no unexpected surprises
  - Behaves as expected with no surprises
    - passes all tests - only if doing tdd
    - Should be this way even with no tests
    - The intended behaviour should be obvious from it's naming and structure
    - Change can be obvious
  - Deterministic
    - does the same thign every time
    - Even for non deterministic systems (like random generators) should have operational or functional bounds that you can define
    - well understood operating characteristics
    - should be able to predict memory, network, storage, or processing boundaries, time boundaries, and expectations on other dependencies.
    - Should have
      - Robustness 
        - is the breadth or completeness of situations that we cover. 
        - Limitations and edge cases should be obvious. 
      - Reliability 
        - is acting as expected in situations that we cover. 
        - should get the same results every time. 
      - Resilience 
        - is how well we handle situations that we do not cover; 
        - unexpected perturbations in inputs or operating environment.
  - Observable
    - in the technical sense - internal state can be infered from outputs
    - Needs to be designed in
      - not added at the end, ie shoehorned in
    - why
      - Gain valuable data and insights about the runtime of the code
    - Types
      - Instrumentation 
        - is your software saying what it is doing.
      - Telemetry 
        - is making that information available, whether by pull—something asking—or push—sending messages; “measurement at a distance”.
      - Monitoring 
        - is receiving instrumentation and making it visible.
      - Alerting
        - is reacting to the monitored data, or patterns in the data.
      - Predicting
        - is using this data to anticipate events before they happen.
      - Adapting 
        - is changing the system dynamically, either to preempt or recover from a predicted perturbation.
  - Reviewing code
    - Is it obvious what this code does, even if it doesn't have any tests or code examples? (And if it doesn't, let's write some characterisation tests to get a feel for how it works.)
    - Does it have suitable instrumentation? (If we don't have a standard for this in the team, this is a good time to start those conversations, too.)
    
## Idiomatic: feels natural

- Everyone has their own coding styles, even if slightly different
  - working within code with different styles adds cognitive load
  - Makes code that should be easy to read for one makes it harder for another to understand
  - For example doing many ways of processing a sequence
    - use an iterator
    - use an indexed for-loop
    - use a conditional while-loop
    - use a function pipeline with a collector (“map-reduce”)
    - write a tail-recursive function
- Instead, use common idioms and conventions either external or internal (team decided) and stick with it
  - might take time to learn, but eventually if stuck with, will be second nature
  - Being consistent in terms of style, shortens learning curve
- This leads to and comes from empathy for your fellow coder
- Not only applies to code, but also to domain
  - Domain terms/names/functions should be similar across similar businesses
    - ie shopping cart, wishlist, basket should be common terms across similar domains, implementations will be different but less cognitive load on learning or following the domain
- The target for your code are those
  - familar with the language, its libraries, its toolchain, and its ecosystem
  - an experienced programmer who understands software development
  - trying to get work done!
- uses language idioms
  - standard features, constructs, libraries ,frameworks, tools
  - feels natural to work with, goes with the grain
  - ie effective javat
- USes local idioms
  - house style, coding standards, design standards, defacto
  - aligned with the project, dependencies, platforms, organsiations
  - Use of Architecture Decision Records define these and automated tests to enforce them
- you can only write idiomatic code if you learn the idioms
- Reviewing code
  - Is this how someone familiar with this technology would write this code? Are we finding it difficult to read, because someone has been "writing Java in Python", or using unnecessarily clever Scala tricks, or solving everything with C++ or Rust macros when simple object composition would be fine?
- Areas of idioms occur at different levels of granuality, ie:
  - naming functions types, parameters, modules
  - layout of code
  - structure of modules
  - choice of tools
  - choice of dependencies
  - how you manage dependencies

## Domain-based: the solution domain models the problem domain in language and structure
- code should convey what it is doing in the language of the problem domain
  - reduce cognitive load
- uses domain language
  - code in the language of the domain, not language of computer science
  - intention revealing, for easy of understanding
    -  to articulate and navigate the solution space in code
  - helps catch bugs
  - remember there are multiple domains
  - Should be able to discuss code where a non coder can understand the code
- use domain structure
  - code for the solution and not the framework
  - payements, loans and not models, views ,controllers
- use domain boundaries
  - as module boundaries, unit of deployment
  - DDD
- Reviewing code
  - Is it using the language of the business domain, or is it using maps, strings, tuples, even tri-state booleans, to represent domain concepts? Can we introduce types or change the names of variables to make it more intention-revealing?
  - Is all the code together that belongs together semantically, or are all the models in one big bag, and the views in another, because that's what the framework authors decided they like?

## Links

- https://cupid.dev/
- https://dannorth.net/2022/02/10/cupid-for-joyful-coding/
- https://speakerdeck.com/tastapod/why-every-element-of-solid-is-wrong?slide=20
- https://www.youtube.com/watch?v=knNaUSLhx-U
- https://mozaicworks.com/blog/cupid-vs-solid
- https://youtu.be/2QahGarHpXQ Daniel Terhorst-North - SOLID vs. CUPID
- https://www.youtube.com/watch?v=cyZDLjLuQ9g CUPID — For Joyful Coding • Daniel Terhorst-North • YOW! 2022

