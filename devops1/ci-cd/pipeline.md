# Pipeline

## CD - continuous deployment

## CI - continuous integration

- First step on pipeline
- On git push, the build is run on a build agent, this allows the app to have a source of truth and place to start from to deploy a working app
- Run all tests
  - Unit
  - acceptance/documentation
  - Integration
  - End to end
  - Tests that dont run locally
    - mutation or long running static analysis tests
    - pacts/consumer contracts
- Creates the binary, ie the jar
- Create the docker image
- Places the binary or image on a Repository

## continuous delivery

## Seperating CI/CD

- PArt of 12 factor app
- The build (CI) creates the binary
- Another pipeline deploys the binary, and is versioned differently
- Should not need to build a new binary to release a new version
  - especially for config changes
- https://12factor.net/build-release-run

## Build Monitor

- A scrreen which displays the all the CI builds, and give visual feed back to what build is failing (coloured red).
- It should be updated constently and not be out of date
- Instant feedback means devs who pushed code that broke build must fix it as a priority, before anyone works on it.
- Should be in a place visible to all the team
- Can have reminders, calendars on it too

## Gocd
- Creating pipelines
- pipelines that pull from git (master or branch)
- manual gates
- materials
- tasks
- jobs
- artifacts
- logs
- Quality gates
  - check status pages

## Teamcity


## Example

https://www.edureka.co/blog/ci-cd-pipeline/

### Jenkins

- https://www.edureka.co/blog/install-jenkins/
