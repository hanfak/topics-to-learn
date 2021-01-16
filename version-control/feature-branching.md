# Feature Branching Development

## Typical workflow for short lived feature branches

Probably not the most opitmal

- From a backlog of stories, typically from the sprint, a free developer will pick up a story.
  - How they choose is dependent on priority, dependency of other stories that need to be finished, size etc
- Create a new branch from master
  - Maybe from Head, maybe from an earlier commit, depends
- When work done and pushed, a build CI is run on that branch
- When story is complete, a pull request is made on that branch
- The request is reviewed, typically by a senior, leaving comments on changes
- A back and forth occurs, where changes are made and reviewed
- When pull request is approved, it is merged with maseter
  - typically done by squashing commits and merging
- CI build is run on master

See Github flow ( https://githubflow.github.io/)

# Usefulness

- feature branches are good when the code has a clear owner, but someone else is doing the work.
  - ie opensource model, whether internal or external (ie github)
  - People all over the place, different timezones,  no communications, working on same codebase


## Long lived feature branches

- https://www.infoq.com/presentations/death-continuous-integration/
- https://www.continuousdeliveryconsulting.com/blog/organisation-antipattern-build-feature-branching/
- https://martinfowler.com/articles/branching-patterns.html
