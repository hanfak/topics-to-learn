# CUPID

An alternative to SOLID

Definitions:

## Composable: plays well with others
  - Code that is easy to use, gets used, used and reused
  - Small surface area
    - less to learn
    - less to go wrong
    - Less to conflict
  - Intention revealing name and purpose
    - easy to discover
    - easy to evaluate
  - minimal dependencies
    - Avoid the whole wanted a banana but got a gorilla holding the banana ie node
    - Avoid adding dependencies which could conflict transitively with clients
  - Reviewing code
    - Does the class/method/function have any dependencies that aren't strictly necessary? If so, how can we remove them, or externalise them and make them optional?
    - Does the code have a small, opinionated interface or API? If not, how can we reduce its surface area?
## Unix philosophy: does one thing well
  - Make each program do one thing well and only one thing
    - "ls" list  flie details, but no inspection of files
  - Together with composability there is nothing you cannot do
    - Expect the output of every program/method to become the input to another
    - pipes , streams api
  - Different to SRP
    - about what code does instead of how the code changes
  - Reviewing code
    - Does each part of the code do one and only one thing, and is it obvious what it doesn't do, and what the edge cases are? If it is doing too much, can we see where to introduce a seam and break things up?
## Predictable: does what you expect
  - Behaves as expected with no surprises
    - passes all tests - only if doing tdd
    - Should be this way even with no tests
  - Deterministic
    - does the same thign every time
    - well understood operating characteristics
  - Observable
    - in the technical sense - internal state can be infered from outputs
    - instrumentation, telemetry, monitoring, alertign, predicting, adpating
  - Reviewing code
    - Is it obvious what this code does, even if it doesn't have any tests or code examples? (And if it doesn't, let's write some characterisation tests to get a feel for how it works.)
    - Does it have suitable instrumentation? (If we don't have a standard for this in the team, this is a good time to start those conversations, too.)
## Idiomatic: feels natural
  - uses language idioms
    - standard features, constructs, libraries ,frameworks, tools
    - feels natural to work with, goes with the grain
    - ie effective javat
  - USes local idioms
    - house style, coding standards, design standards, defacto
    - aligned with the project, dependencies, platforms, organsiations
  - you can only write idiomatic code if you learn the idioms
  - Reviewing code
    - Is this how someone familiar with this technology would write this code? Are we finding it difficult to read, because someone has been "writing Java in Python", or using unnecessarily clever Scala tricks, or solving everything with C++ or Rust macros when simple object composition would be fine?
## Domain-based: the solution domain models the problem domain in language and structure
  - uses domain language
    - code in the language of the domain
    - remember there are multiple domains
  - use domain structure
    - code for the solution and not the framework
    - payements, loand and not models, views ,controllers
  - use domain boundaries
    - as module boundaries, unit of deployment
    - DDD
  - Reviewing code
    - Is it using the language of the business domain, or is it using maps, strings, tuples, even tri-state booleans, to represent domain concepts? Can we introduce types or change the names of variables to make it more intention-revealing?
    - Is all the code together that belongs together semantically, or are all the models in one big bag, and the views in another, because that's what the framework authors decided they like?

## Links

- https://dannorth.net/2022/02/10/cupid-for-joyful-coding/
- https://speakerdeck.com/tastapod/why-every-element-of-solid-is-wrong?slide=20
- https://www.youtube.com/watch?v=knNaUSLhx-U
- https://mozaicworks.com/blog/cupid-vs-solid
- https://youtu.be/2QahGarHpXQ Daniel Terhorst-North - SOLID vs. CUPID
