# Unit testing

- Not well defined, many different meanins of unit
- it's a situational thing - the team decides what makes sense to be a unit for the purposes of their understanding of the system and its testing.

## Speed 

- feature of unit testing 
- The faster the better
- generally involves replacing slow collaborators with test  doubles
-  test suites should run fast enough that you're not discouraged from running them frequently enough.

## what 
- Probably best to be called Isolation Tests
  - opposite of integration tests
- There are many definitions, mainly due to the ambiguous nature of the word unit
  - https://martinfowler.com/bliki/UnitTest.html
  - https://srikanth.sastry.name/defining-unit-tests-two-schools-of-thought/
  - Properties
    - https://www.youtube.com/playlist?list=PLlmVY7qtgT_lkbrk9iZNizp978mVzpBKl
    - Isolated — Unit tests are completely isolated from each other, creating their own test fixtures from scratch each time. (Note that I’m not saying these are the only useful tests, just that if tests aren’t isolated you’re going to have a hard time making the case that they are “unit tests”.)
    - Composable — Follows from isolation.
    - Deterministic — Should be. Code that uses a clock or random numbers should be passed those values by their unit tests.
    - Specific — If a unit test fails, the code of interest should be short.
    - Behavioral — If the behavior changes accidentally, a unit test should fail.
    - Structure-insensitive — This can be a challenge for unit tests. Too much mocking, especially strict mocking, is a structure sensitivity nightmare.
    - Fast — Yep.
    - Writable — Good interface design makes writing unit tests easier. Alternatively, difficult-to-write unit tests are the canary in the bad interface coal mine.
    - Readable — It can be challenge to write readable unit tests, because you are seeing so little context compared to the whole system.
    - Automated — Yep.
    - Predictive — Unit tests passing likely gives little confidence that the whole system is working. Unit tests failing should give great confidence that the whole system is not working.
    - Inspiring — A frequently-run unit test suite gives great confidence the programming is progressing. Sometimes I run my unit tests 2 or 3 times, just because it feels good (and they’re wicked fast).
- there is the case of testing every behaviour a class does
  - but this can lead to highly coupled test code
- APPROACH 1. Unit Testing Use Cases (Uncle Bob)
  - In Clean Architecture (Uncle Bob), the use cases are independent of any out-of-process dependencies, i.e., independent of the database, SMPT, messaging bug, and third-party systems.
  - We can thus unit-test the use cases by mocking out any out-of-process dependencies.
  - the Use Case Unit Tests indirectly cover the Domain (hence there are no Unit Tests targeting the Domain per see).
- APPROACH 2. Integration Testing Use Cases & Unit Testing Domain (Khorikov)
 - In Unit Testing (Vladimir Khorikov), Khorikov distinguishes between managed out-of-process dependencies (e.g., database) versus unmanaged out-of-process dependencies (e.g., SMTP, message bus, third-party systems). Use Cases are implemented through Controllers (Application Service Layer). These controllers have a direct dependency on the database (e.g., reference the ORM), and interfaces are used only for unmanaged dependencies.
 -  we apply a two-level approach for testing the Use Cases. The Use Cases are tested via Integration Tests (unmanaged dependencies are mocked out, but managed dependencies are not mocked out). The Domain is tested via Unit Tests.
- Approach 1 vs Approach 2
  - Which is more optimal? Do we use a hybrid?
  - What about combinatorial explosion?
    - should this be tested at lower/specific level

## I/O Free vs I/O Dependent

- https://ted.dev/articles/2023/04/02/i-m-done-with-unit-and-integration-tests/
- Instead of using the confusing names of unit and integration tests (where differences in meanings cause confusion)
- Use **I/O Free** which defines sociable or class specific tests that dont talk to any I/O
  - Can include library we use 
    - in java, the use of collections is still library but we dont mock it
    - So even individual class tests, still uses the library as they are not mocked (sociable tests)
  - No I/O is fast and predictable/deterministic
  - Improves speed of TDD, by gettign fast feedback
  - If the majority of these are used, faster builds
  - Any I/O is stubbed or use a fake in place of adapters (who talks to I/O)
    - or use Nullables
      - https://www.jamesshore.com/v2/projects/nullables/a-light-introduction-to-nullables
    - AVoid mocking, improve ease of refactoring and reduce integration issues with libraries
  - In hexagonal arch, can take advantage of the dependency inversion and isolate the usecases (core of app) from I/O and write tests at this layer and new everything up and fake all I/O integrations 
    - any class that has complex rules that is called on by an usecase, can be tested in isolation
- I/O dependent includes 
  - database 
  - files 
  - Across network (queues/bus/http/rpc etc)
  - time/date 
  - randomness
- Need to have **I/O Dependent tests**  
  - These are slower, hard to write, unpredictable, lots of setup
  - Use of test containers help, esp for DB/queues, but still slow
    - Cannot use for external serivce say API - but can use a service virtualisation (wiremock)
  - Needed to show things work, up to a limit
    - Can only do so much, as need to test in sandbox environment which actually talks to real db/services 
  - This can be bottom of stack
    - where the integration points happen (talk to the db)
  - or top of the stack 
    - bring the whole app and having these I/O services up
  - Can be separated from I/O free tests, and run after them during a build

## Solitary vs sociable 

- A way of writign unit tests 
- 
### solitary tests
  - writing unit tests at the class/function level 
  - where all dependencies are replaced by test doubles 
    - class under test is run in total isoalation
  - Mockists school

#### pros 

- Isolates issues: 
  - Solitary unit testing can help to isolate issues to a specific unit or component, making it easier to identify and fix issues.
- Simplifies testing: 
  - Solitary unit testing can simplify the testing process, as each unit can be tested independently without requiring coordination with other units or components.
- More granular: 
  - Solitary unit testing allows for more granular testing, as each unit can be tested thoroughly in isolation.

#### Cons

- May miss integration issues:
  - Solitary unit testing may not catch issues that only arise when units are combined in a real-world scenario.
- Can be time-consuming: 
  - Solitary unit testing can be time-consuming, as each unit must be tested separately, which can result in a large number of tests.
- May not fully test system behavior:
  - Solitary unit testing may not fully test the behavior of the system as a whole, as it does not test the interaction between components.


###sociable test 

- where groups of interconnected units or components are tested together as a group, rather than testing each unit in isolation.
- writing unit tests at the class/function level
- where only IO dependencies, randomness, time are replaced by test doubles ie awkward collaborators and remove randomness
  - all other dependencies are instantiated
- Classic school

#### pros

- Tests the interaction between components: 
  - Sociable unit testing can identify issues that may not be caught by testing individual units in isolation. 
  - Testing the interaction between components can help uncover issues that may arise when different components are combined in a real-world scenario.
- Can be more efficient: 
  - In some cases, testing a group of interconnected components together can be more efficient than testing each component in isolation, as it can reduce the need for redundant or overlapping tests.
- Better mimic real-world scenarios: 
  - Sociable unit testing can better mimic real-world scenarios and can provide a more accurate representation of how the software will function in the real world.
  
#### Cons

- Can be more complex:
  - Sociable unit testing can be more complex and difficult to implement than testing individual units in isolation. 
  - It can be more difficult to isolate issues and to identify the root cause of issues that arise during testing.
- Requires a more comprehensive understanding of the system: 
  - Sociable unit testing requires a more comprehensive understanding of the system and its components, and can require more coordination between developers and testers.
- May miss certain issues: 
  - Sociable unit testing may miss certain issues that could be caught through testing individual units in isolation, such as issues that only arise when certain units are combined in a specific way.
  

## Rules of unit testing 

- https://www.artima.com/weblogs/viewpost.jsp?thread=126923
- A test is not a unit test if:
  - It talks to the database
  - It communicates across the network
  - It touches the file system
  - It can't run at the same time as any of your other unit tests
  - You have to do special things to your environment (such as editing config files) to run it.


## Links 

- https://martinfowler.com/bliki/UnitTest.html