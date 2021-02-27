# Vertical Slice architecture

## What?

- “vertical slice” being a crossection of code that runs from the front-end deep down to the data layer
- The goal is to minimize coupling between slices and maximize coupling within a slice.
-  is built around distinct requests, encapsulating and grouping all concerns from front-end to back.
-  Vertical Slice Architecture aims to separate the code by features, aiming to minimize code sharing between features.
- similar idea to microservices, but no talking between each other
- It focuses not on the separation of concerns from a technical perspective (like domain vs. infrastructure vs. application logic) but from the perspective of reflecting the business domain’s features.



## Why/benefits

- Covers issues found in onion/layered architecture
  - these architectures  tend to be mock-heavy, with rigid rules around dependency management
  - Exposion of abstractions that are not needed
-  treat each request as a distinct use case for how to approach its code.
- More teams can work on different parts of the code (different use cases) with out intefering with each other (ie merge issues)
- Context switching becomes less of a problem as everything related to that feature is in the current namespace. There’s no need to follow code down a rabbit hole across the application.
  - the benefit of file proximity
  - the principle of high cohesion: things that change together ought to live together.
  - Less confusing to new developers
- Change requests from users or the business tend to be vertical in manor, so it makes sense to architect our application vertically as well. It is not often that you get a change request for something that is horizontal in nature.
- Dont need abstractions early on (yagni), can leave for later
  - Dont need to change external dependencies, so planning for this might not be necessary
- Each vertical slice can have different dependencies (similar to microservices)
  - ie one slice can use sql another can use orm
- Liftability, can copy slices to other projects

## Common patterns invovled

- SOLID in sliced https://www.youtube.com/watch?v=wTd-VcJCs_M

## How

- Vertical slices should be isolated. One vertical slice should not reach outside of it’s namespace and it should definitely not call into another vertical slice.

## Testing

## Downsides

- can lead to a lot of duplication
  - Need to have some form shared code that reduces duplication, but can lead to issues if multiple people working on it
- Testing becomes hard at unit level, as less indirection (interfaces for dependencies), hard to mock a database dependency and test business logic in memory
  - More end to end testing of whole slice
- If using pure slices, then domain (objects and language) used could end up being different in different slices within same app
  - Use shared domain model

## Links

-  Jimmy Bogard https://www.youtube.com/watch?v=SUiWfhAhgQw
-  Jimmy Bogard same https://www.youtube.com/watch?v=T6nglsEDaqA
-  https://blogs.cuttingedge.it/steven/posts/2011/meanwhile-on-the-command-side-of-my-architecture/
-  https://blogs.cuttingedge.it/steven/posts/2011/meanwhile-on-the-query-side-of-my-architecture/
-  https://jimmybogard.com/vertical-slice-architecture/
