# Trunk Based Development

- Work directly on master branch
- Use short lived feature branches
- Need team wide practices to do this
- A source-control branching model, where developers collaborate on code in a single branch called ‘trunk/master/main’, resist any pressure to create other long-lived development branches by employing documented techniques. They therefore avoid merge hell, do not break the build, and live happily ever after

## Benefits
  - Real time feedback
    - face to face feedback
      - pull requests occur in written form, which can be tedious to write (thus not everything is written), can cause conflict due to coders owning the code, the comments are not nuanced or clear or open for discussion.
    - Later feedback in pull requests are too late to make substantial changes (ie design/architecture)
  - Team wide code
    - No single point of failure, easier to build knowledge of code and domain, less likely to be defensive about code base and willing to change and accept ideas
  - Established coding practices with in code base
    - The code base should look like it was written by one person, easier to integrate new team members, easier to follow/read code and make changes, establish good practices,
  - Continuous integration
    - key enabler
    - With feature branching, pushed to master at the end, rather continously, this can lead to issues on the maste CI build
    - Trunkbased, always pushing to master, getting fast feed back, and master is always upto date
    - Broken builds are top priority
      - Always pushing code in non breaking fashion, ie local builds always pass before pushing
      - With feature branching, easier to ignore failing builds until pull request
  - Not breaking things
  - Code base is up to date
  - Visibility of what everyone is doing
    - Everyone is upto date on what everyone is doing, and can spot when to help
  - Use IDE for  reviewing changes
    - it is far better than using a web browser
  - Easier to veiw history
    - preserve changes and commit history. The commits are a sort of documentation. Helps in understanding the code, fixing issues/bugs,
  - Easier to refactor
    - working on a branch, people dread doing refactorings or anythign that will cause merge conflicts ie renaming packages, moving things around, architectural changes.

Working directly on master means the team must know
- how to work without breaking code
- how to write good tests
- how to work together effectively, etc.

See the book Accelerate, and trunk based development is a sign of high performance

People work feature branches because
  - Want to keep master in good state
  - Want to review others code
  - But most of the time **It’s easier and more efficient if everyone works in their own branch, so we don’t tread on each other’s toes**

Feature branching, focuses on individual productivity, rather than team productivity. In terms of lean, this is optimising for resource efficiency rather than for flow efficiency. Trunk based, can look like individuals are going slower, but the team goes faster.

## Key practices for trunk based development

- Pair programming
  - Code is being review in real time
  - other benefits see [here](../../management-workflow/pair-programming.md)
- Build that can be trusted
  - local/CI builds are fast and give trust that this version is good to be used by other teams to work on, or can be deployed to test environment
  - Follow testing pyramid
  - Follow TDD & BDD
  - Fixing build is priority
    - If not quick to fix, then revert changes and push to CI
- Use branch by abstraction
- Use feature flags
  - https://martinfowler.com/articles/feature-toggles.html
  - Add feature without, and have a toggle (part of config), so code does not need to be changed

## Example of trunk based workflow

- Developers pair full time.
- One pair of developers picks up a new story. As part of the definition for getting ready for development, they write the skeleton of one or more acceptance tests, and a list of tasks for the story.
- When the pair thinks that they are ready, they gather the team and show everyone the acceptance tests, with the intent of confirming that everyone has the same understanding of what the story is about and what the team is about to implement. This is called BDD, where we use examples to create shared understanding.
- Each pair of developers picks a task from the story. Most of the times we had 2 or 3 pairs working on the same story, simply picking independent tasks.
Each pair commits and pushes straight to master, at a frequency that ranges from a few minutes to a few hours. They commit every time that they get to a green state: red-green-refactor, commit and push. We all loved small, frequent, commits, with clear messages indicating *why* we had just done a particular change. The commit message ideally uses business terms and focuses on the business outcome that we are trying to achieve with that commit. A good example is “Implemented the acc. test to prove that only a single customer can be allocated to a port”, or “Renamed class, since we discovered that the rest of the business refers to a ‘room’ as a ‘colo space’”.
- Whenever developers pull from git they rebase in order to keep commits in the same order as they happened in real life.
- Before a commit, the pair always runs a local build to ensure it’s successful. The build usually takes anywhere between 30 seconds and 2 minutes.
- We followed the testing pyramid for our testing strategy, always preferring faster tests over slow ones. Our effort was greatly facilitated by the use of clean architecture, which allowed us to keep business logic isolated from technical details. It’s not the only way, but it worked great for us.
- At any point in time the codebase is always releasable, by using the “branch by abstraction” pattern. In practice, being a Java project, we simply didn’t wire in the Spring beans until the very last minute. All the new code was available to test, but not used in production until we were ready to wire it in.
- Whenever code is pushed, the CI tool builds it and runs all tests. We didn’t automatically deploy anywhere, but we could have done if we wanted to.
- Development of a story usually was completed after a few days. At this point, we gathered around the team again to showcase what had just been implemented.
- The latest version of the application would now be released into a staging environment, where our QA expert would perform some exploratory testing (typically lasting from a few hours to a few days).
- If no surprises came up, the application was then promoted into production (typically the next day).
- In the meantime, towards the end of the development of the previous story, one pair would have started looking at the next story to get it ready and keep a good flow. We used work-in-progress limits to keep this flow under control.
- If at any point one pair felt the need to discuss something as a team (e.g. architectural decisions; design; trade-offs) they would simply ring a bell to grab everyone’s attention. All pairs would gather for an impromptu mob-programming session, spiking the solution out together. When everyone was happy the pairs would split again.


## Links

- https://medium.com/@mattia.battiston/why-i-love-trunk-based-development-641fcf0b94a0
- https://www.continuousdeliveryconsulting.com/blog/organisation-pattern-trunk-based-development/
- https://trunkbaseddevelopment.com/
