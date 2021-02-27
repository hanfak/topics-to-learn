# Outside in

- Outside in development combines the principles of test driven development and acceptance driven development into one approach.
- is an approach that focuses on building just enough well-engineered code to satisfy an external need, reducing accidental complexity by removing speculative work.
- Code should only be written to satisfy an external need, being from a user, an external system, or another piece of code
- Drive development from the interface (ui/api)

## How

- It starts with a developer taking a Gherkin (some spec) example and connecting it to failing automation code that is failing because it is attempting to interact with production code that doesn’t exist yet. With the failing example in place a developer could then write all the production code to make the test pass, and then refactor (whilst ensuring the test stays green). This is known as the "outer circle" of outside in development.
- For UI, mock ups are used and created collaboratively
  - used agree on the user journeys and the data the users will be interacting with during each journey.
- Once the UI is done, we are ready to slice the backend work in vertical increments. Each vertical increment should start from a user interaction and contain all the logic (persistence, communication with external systems, etc.) needed to satisfy that user interaction. Once this increment is finished, the system will have a new behaviour added to it.
- API design should be driven by the needs of the clients of the API and not by what backend developers think API clients will need.

## Aims

  - Value is only delivered when the system is in production and satisfactorily used.
  - We should strive to deliver value as soon and as often as possible.
  - We should do the appropriate due diligence before building anything.
  - We should get feedback as soon and as often as possible.
  - We should always work in small and valuable increments.
  - We should keep things as simple as possible, but no simpler.
  - We should only build what really needs to be built, nothing more.
  - We should not work on technical tasks if they do not have business value.
  - Investigative work should be time-boxed and done as separate a task.

## Benefits

- Promote vertical slice architecture
  - Easy of development for multiple teams working on same codebase
- Focused coding
  - provide functionality that is requested
  - Know when done
  - reduces over enginneering
  - using mock ups help team all agree with the UI/interface, so we will know the exact behaviour the backend will need to provide and will have a more well-defined and stable domain language
- Everything is wired up from the start
  - For code to be complete, eveything is linked up to provide the feature
- Better for cross functional teams
- When feature is coded, it is done
  - no waiting for UI  to be done
  - Downstream dependencies are done before being used (although this may change as work is done)
- easily define the boundaries for acceptance tests and use them to guide our development.

## Differences

The differences between the ATDD approach and outside in development are:
  - In outside in development the source of the ‘acceptance tests’ come from captured examples from a conversation and not recorded expectations from a single source such as a business analyst or developer.
  - Rather than jump straight in and create production code, the developer will move into the inner circle and adopt a test driven development approach to create tests for each unit of the code production code required to make the outer circle go green.

## Links

- notes on sandro doing outside in on bank kata https://gist.github.com/xpepper/66ced102032ad479b8170d9205754519
- Sandro Mancuso https://www.youtube.com/watch?v=bvie9vl7X6A
  - Related blog post https://www.codurance.com/publications/2017/10/23/outside-in-design
- https://8thlight.com/blog/georgina-mcfadyen/2016/06/27/inside-out-tdd-vs-outside-in.html
