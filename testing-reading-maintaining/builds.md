# Builds

- What is it?
  - A way of running all your tests
  - packaging a deployable app (ie jar, docker image)
  - Compile application, test sources, resources
  - Run any pre requirements for build or creating app ie recreating database or environment variables
  - Store app/jar and metadata on local class path (to use as library in other app)
  - Store app/jar and metadata on external repository (ie artifactory/ maven central)
  - Can have separate steps of build, ie run separate steps, run database recreate

- Types of build libraries
  -  Maven
  - Gradle
  - Ant
  - Bash scripts

- Use a build wrapper
  - This is some extra files, which allows any user to run the build tool (and its functions) on any machine, by fixing the build tool version (and downloading it if necessary)

- Aim
  - Should run before commiting the code changes, makes sure all tests are passing, past behviour is not breaking.
  - Can run on CI step (ie when pushed changes to repo (Github), runs the build to makes sure this the version and application that can be deployed to an environment ie prod/test)
  - Build should be as short as possible
    - Reduce amount of I/O operations locally
      - ie html output of acceptance tests is not need for local build, but for CI build (so that analysts or testers can read the documentated tests)
    - Reduce the amount of expensive objects/actions (take time to load/create)
      - ie create the server of the application only once, instead of doing for each test or test class. If using a live server, run the application at the beginning of all the tests that need it.
      - The in the app should use object pooling for expensive objects, ie database connections
    - Reduce the amount of network calls
      - tests should use a stub
        - call a mock of a  class which does the http calls
        - Call the methods via http and not over tcp/ip
        - Have another server up and running where the calls make a http/tcp/ip call to
    - Reduce the amount of database calls
      - tests should use stub ie map/array
      - Use test database, not prod (test containers)
    - Use the testing pyramid
      - There should be integration tests to check integration points are working ie database calls are working
      - End to end tests, to check the full flow
        - Have an up and running database, network calls to a stub (ie wiremock)
    - Run tests concurrently.
      - Run concurrently in the same jvm
      - Run concurrently on multiple jvms
  - Build should give quick feedback
    - Should fail fast
    - Give good feedback
      - use good testing framework with good feedback
      - logs should be enabled
  - Tests should not interfere with each other
    - Tests should not share state with each other, so can be run in parallel

## Issues with running build

- Running a build means running all your tests to make sure that specific build is a candidate for deployment
- The larger the project gets (or more features it adds) the number of tests increases
- This leads to long build times, either locally or on CI. Which is bad for fast feed back
- How to decrease time taken to improve lower time of build
  - Separate unit tests from end to end and integration Tests
    - Run unit tests first, this will be fast, and if this fails get fast feed back
    - The longer running tests (E2E and integration) are run later, after the unit tests pass
    - This may mean separating unit tests into one module and E2E and integration tests into anothe module. where the jars/binaries are run during separate stages of the build
      - Probably not best for early stages of projects
    - Can use build tool to run different packages, and to fail fast depending on the package, and order what packages to test first
      - surefire and failsafe for maven
  - Reduce the number of integration, E2E and module tests
    - edge cases, lots of different cases can be done via a unit test
    - Add a link between the tests to keep track
    - One E2E for one case, and several unit/documentation tests for the other cases (as long as they follow same logic and flow within app)
  - Do not replicate tests, if acceptance test tests a flow, do not repeat with unit or integration test.
    - If turning unit test to documentation test delete the unit test
  - Do not create the output (ie html) when running a local build but do it for CI
  - Run tests in parallel
    - easier for unit tests with mocks
  - Run only tests which affect changed, deleted or new methods/classes - dynamic tests
    - https://engineering.shopify.com/blogs/engineering/spark-joy-by-running-fewer-tests
  - Reduce start up time of tests
    - if running E2E test and takes time to start up app, then keep the app for all the other tests
      - Will need to return the app to clean state before each test though
    - Use a docker container of the app, keep the container running until all the tests have finished
