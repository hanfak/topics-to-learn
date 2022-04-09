# Choosing A Language

- Depends on the type of application you are building
- There will always be trade offs
- First decision, and most costly if need to change due to lack of features/capabilities the further down the road
  - Example of changing is Twitter moving from Ruby to JVM https://www.infoq.com/articles/twitter-java-use/
- Necessary to think about when starting a greenfield project.
  -  A project already made, ie brownfield, you will not change the language but use the exisitng one. Only relunctly and if there are very good reasons to.
- No language is perfect, and there are costs in learning and hiring
- Criteria
  - technical qualities
    - ie support for concurrency
    - How the language works and does that help your situation
    - Dont need to have the best langugae, but should filter out the langugaes that wont help you achieve your aims
  - Popularityy
    - Good documentation, solutions easily found
    - lots of maintained libraries
    - Supported by strong community opensource/paid by volunteers or companies
    - Ease to hire
  - Community
    - Good developers, easy to hire
    - Good practices, less mistakes
  - Platform used
    - microsoft or apple or unix
  - Staff
    - knowledge/skills base
- Areas
  - enterprise
    - jvm (java/kotlin/scala), c#, c/c++
  - academic
    - python, julia, R, matlab, mathematica, prolog, haskell
  - Concurrent/reliable
    - erlang, go, elixir
  - systems
    - c/c++, rust
  - Game development
    - c++, C#
  - Rapid And Productive Web Development
    - javascript, typescript, php
  - Apple
    - swift, objective c
  - All purpose
    - c#, java

- Links
  -  https://tomassetti.me/best-programming-languages/
  - https://softwareengineering.stackexchange.com/questions/122900/how-managers-choose-programming-languages
  - https://eng.uber.com/tech-stack-part-one/

## For enterprise

- concerns
  - Secruity
    - not vulnerable to secruity attacks
  - Scalability
    - Handle rising user demands in the future
  - Robust
  - Access to lots of data
  - Integration with existing systems
  - Operational efficiency
    - speed and performance of the application
    - money spent is worth it
  - Skillset
  - Development speed
    - in creating features, maintaining and fixing bugs
  - Reputation
    - built and maintained by a company
- large software systems built on dynamically typed and interpreted languages have all kinds of issues from correctness to performance.

### Why use java

- widely used
- older systems written in java
- backwards compatibility, stable platform
- support from owner and community
- Mature libraries and frameworks, and lots of them
- Easy to hire, comp sci grads learn java
- Highly scalable, good support for concurrency, multithreading
- Good testing libraries
- Good support for integration (servlets/http, message brokers)
- Good integration with databases
- platform independent
- No licensing costs (if on non oracle)
- statically typed, compiler spots problems first
- Great IDEs
- Good build tools (maven)
- JVM, tooling (jconsole), efficient garbage collection, memory management
- Easy to learn
- Better secruity

links

- https://www.devteam.space/blog/why-should-you-use-java-for-your-backend-infrastructure/


### Problems with Javascript/NodeJS

### Problems with Python

- Migrating to new versions
- Low performmace
  - there are implementations that run on the jvm
- Difficult to deploy
  - https://www.nylas.com/blog/packaging-deploying-python/
- Scalability issues due to global interpreter log
- Dynamically typed
  - no support from compiler, problem occurs at runtime
  - hard to refactor
  - hey’re much more costly to debug
-  GC tuning and memory management strategies are much more mature in JVM than Python (which only provides a basic interface)
- hat most unattended 24x7 software systems require monitoring, and this is not yet part of CPython to the extent it is supported in JVM for instance. While you can build your own metrics in Python and expose them, JVM has them ready.
- Another disadvantage is scalability. There is something called global interpreter log. This thing ensures that from a given process nothing can really run in parallel without spawning a complete new process which is expensive.

links

- https://www.analyticsindiamag.com/why-has-python-failed-to-penetrate-the-enterprise-development-sector/
- https://www.sayonetech.com/blog/can-your-enterprise-choose-python-software-development/

## Ideal languages

- https://www.youtube.com/watch?v=MPyUvtPFDSg The Ideal Programming Language • Richard Feldman & Erik Doernenburg • GOTO 2021
