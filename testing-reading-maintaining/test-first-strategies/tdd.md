# Test driven development (TDD)

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Test driven development (TDD)](#test-driven-development-tdd)
	- [What??](#what)
	- [When??](#when)
	- [Why?](#why)
	- [How?](#how)
		- [How to solve problems in implementing](#how-to-solve-problems-in-implementing)
	- [Common Mistakes](#common-mistakes)
	- [Links](#links)

<!-- /TOC -->

## What??

-  testing methodology or a programming practice implemented from a developer’s perspective.
- attempts to answer a simple question – Is the code valid?
- The main intention of this technique is to modify or write a fresh code only when the test fails.
- technique is largely popular in agile development ecosystems.

## Benefits

- Helps reduce the amount of time required for rework
- Helps explore bugs or errors very quickly
- Helps get faster feedback
- Encourages the development of cleaner and better designs
	- Reduces intelligent code for more maintainable and readable code
- Enhances the productivity of the programmer
- Allows any team member to start working on the code in the absence of a specific team member. This encourages knowledge sharing and collaboration
	- Shows how the unit works and should do
- Gives the programmer confidence to change the large architecture of an application easily
- Results in the creation of extensive code that is flexible and easy to maintain
- results in lesser duplication of test scripts
- Reduces manual testing
- Enforces discipline
- No prod code is written without being tested

## How?

- Red -> Green -> Refactor -> Repeat until all behaviour has been done
- Based on the requirements specified in the documents, a developer writes an automated test case
- These tests are executed, and in most cases, they fail as they are developed before the development of an actual feature
- The development team then refactors or changes the code for the test to pass successfully
- With a set of passing tests, the developers refactor code to improve design without adding any behaviour
- https://www.linkedin.com/posts/oliver-zihler_testdrivendevelopment-tdd-extremeprogramming-activity-6974718936256761856-EXqV/

## Issues

- Mocking external services (ie database calls, io) only, does not check whether the external service work, but just checks the type.
	- Can have integration tests, if the external service is wrapped
	- Have a system/end to end tests which check these integration points
- The desire for code coverage, can lead to mocking and verifying something was called, but not checking it actually works
- TDDing UI can be difficult
	- UI testing is mainly about looks and feels, thus difficult to test
- Can take time, and more complex testing(system) even longer esp with initial setup
	- But time is made up, via less bugs, can refactor wiht safety
	- it is not instant and can slow down initial development
- Tests are code, and this needs to be maintained

## Design and TDD

- Sandro  https://www.youtube.com/watch?v=KyFVA4Spcgg

### How to solve problems in implementing

- https://completedeveloperpodcast.com/episode-53/

## Common Mistakes

- The Liar
	- An entire unit test that passes all of the test cases it has and appears valid, but upon closer inspection it is discovered that it doesn’t really test the intended target at all. No useful or any assertions
	- Found when chasing test coverage and not practising TDD
	- Gives the illusion of coverage
	- Delete test without coverage
	- If no assertions, add them
- Excessive Setup
	- A test that requires a lot of work setting up in order to even begin testing. Sometimes several hundred lines of code is used to setup the environment for one test, with several objects involved, which can make it difficult to really ascertain what is tested due to the “noise” of all of the setup going on.
	- shows poor separation of concerns and modularity
	- Test and code becomes highly coupled, so changing one affects the other, projects grind to a halt
	- Hard to maintain
	- Start to add abstractions, SRP,
- The Giant
	- A unit test that, although it is validly testing the object under test, can span thousands of lines and contain many many test cases. This can be an indicator that the system under tests is a God Object
	- These tests become difficult to understand
	- Highly coupled and fragile tests
	- Have multiple tests, with one assertion per test
	- Hard to understand what went wrong
- The Mockery
	- Sometimes mocking can be good, and handy. But sometimes developers can lose themselves and in their effort to mock out what isn’t being tested. In this case, a unit test contains so many mocks, stubs, and/or fakes that the system under test isn’t even being tested at all, instead data returned from mocks is what is being tested.
	- Can result from excessive setup
	- Need to have tests on the behaviour of the object under test, the object under test must do something then test the output or side affects
	- Dont test what you primed
- The Inspector
	- A unit test that violates encapsulation in an effort to achieve 100% code coverage, but knows so much about what is going on in the object that any attempt to refactor will break the existing test and require any change to be reflected in the unit test.
	- NEver compromise the encapsulation for testing
	- No code should be created in prod, to just be used in tests
- Generous Leftovers
	- An instance where one unit test creates data that is persisted somewhere, and another test reuses the data for its own devious purposes. If the “generator” is ran afterward, or not at all, the test using that data will outright fail.
-	The Local Hero
	- A test case that is dependent on something specific to the development environment it was written on in order to run. The result is the test passes on development boxes, but fails when someone attempts to run it elsewhere.
- The Nitpicker
	- A unit test which compares a complete output when it’s really only interested in small parts of it, so the test has to continually be kept in line with otherwise unimportant details. Endemic in web application testing.
- The Secret Catcher
	- A test that at first glance appears to be doing no testing due to the absence of assertions, but as they say, “the devil’s in the details.” The test is really relying on an exception to be thrown when a mishap occurs, and is expecting the testing framework to capture the exception and report it to the user as a failure.
- The Dodger
	- A unit test which has lots of tests for minor (and presumably easy to test) side effects, but never tests the core desired behavior. Sometimes you may find this in database access related tests, where a method is called, then the test selects from the database and runs assertions against the result.
- The Loudmouth
	- A unit test (or test suite) that clutters up the console with diagnostic messages, logging messages, and other miscellaneous chatter, even when tests are passing. Sometimes during test creation there was a desire to manually see output, but even though it’s no longer needed, it was left behind.
- The Greedy Catcher
	- A unit test which catches exceptions and swallows the stack trace, sometimes replacing it with a less informative failure message, but sometimes even just logging (c.f. Loudmouth) and letting the test pass.
- The Sequencer
	- A unit test that depends on items in an unordered list appearing in the same order during assertions.
- Hidden Dependency
	- A close cousin of The Local Hero, a unit test that requires some existing data to have been populated somewhere before the test runs. If that data wasn’t populated, the test will fail and leave little indication to the developer what it wanted, or why… forcing them to dig through acres of code to find out where the data it was using was supposed to come from.
- The Enumerator
	- A unit test with each test case method name is only an enumeration, i.e. test1, test2, test3. As a result, the intention of the test case is unclear, and the only way to be sure is to read the test case code and pray for clarity.
- The Stranger
	- A test case that doesn’t even belong in the unit test it is part of. it’s really testing a separate object, most likely an object that is used by the object under test, but the test case has gone and tested that object directly without relying on the output from the object under test making use of that object for its own behavior. Also known as TheDistantRelative.
- The Operating System Evangelist
	- A unit test that relies on a specific operation system environment to be in place in order to work. A good example would be a test case that uses the newline sequence for windows in an assertion, only to break when ran on Linux.
- Success Against All Odds
	- A test that was written pass first rather than fail first. As an unfortunate side effect, the test case happens to always pass even though the test should fail.
- The Free Ride
	- Rather than write a new test case method to test another feature or functionality, a new assertion rides along in an existing test case.
- The One
	- A combination of several patterns, particularly TheFreeRide and TheGiant, a unit test that contains only one test method which tests the entire set of functionality an object has. A common indicator is that the test method is often the same as the unit test name, and contains multiple lines of setup and assertions.
- The Peeping Tom
	- A test that, due to shared resources, can see the result data of another test, and may cause the test to fail even though the system under test is perfectly valid. This has been seen commonly in fitnesse, where the use of static member variables to hold collections aren’t properly cleaned after test execution, often popping up unexpectedly in other test runs. Also known as TheUninvitedGuests
- The Slow Poke
	- A unit test that runs incredibly slow. When developers kick it off, they have time to go to the bathroom, grab a smoke, or worse, kick the test off before they go home at the end of the day.
- The Cuckoo
	- A unit test which sits in a test case with several others, and enjoys the same (potentially lengthy) setup process as the other tests in the test case, but then discards the some or all of the artefacts from the setup and creates its own
- The Mother Hen
	- A common setup which does far more than the actual test cases need. For example creating all sorts of complex data structures populated with apparently important and unique values when the tests only assert for presence or absence of something
	- This can be a sign that the setup was written before the tests themselves, which is a subtle bit of up-front design easily hidden in an otherwise fully TDD process.
- The Wild Goose
	- A unit test which, even though it initially appears simple, seems to require an ever increasing amount of the application to be created or initialised in order to make it pass.
	- This sort of test can take up a disproportionate amount of developer time, and lose the benefits of the fast turn-round TDD cycle. In the worst case, TDD is effectively abandoned while the all or most of the application is developed using an untested up-front process to make a single test pass.
	- This is common among developers new to TDD who are not yet comfortable with “faking” a response before moving the focus of design to a lower level.
- The Homing Pigeon
	- A unit test which (typically because it requires non-public access to a class under test) needs to be created and run at a particular place in a package hierarchy. This initially seems perfectly reasonable, but can unexpectedly fail if the class under test is moved to a new location or (worse) split so that its behaviour goes to more than one such location
	- It should probably be noted that this is still an active area of discussion, with many people arguing that it is a necessary or even benficial approach to design by allowing testing of non-public access.
- The Dodo
	- A unit test which tests behavior no longer required in the application. Both the behaviour and the test should probably be deleted.



## Links

- intro https://technologyconversations.com/2013/12/24/test-driven-development-tdd-best-practices-using-java-examples-2/
- example and intro https://www.youtube.com/watch?v=PIWLC3dexSA
- jbrains tutorial https://online-training.jbrains.ca/courses/wbitdd-01/lectures/133270

- outside in testing https://www.youtube.com/watch?v=XHnuMjah6ps

- marsrover https://www.youtube.com/watch?time_continue=4119&v=24vzFAvOzo0
- https://www.freecodecamp.org/news/test-driven-development-what-it-is-and-what-it-is-not-41fa6bca02a2/
- https://www.codurance.com/publications/2016/06/14/mastering-tdd

https://medium.com/javascript-scene/the-outrageous-cost-of-skipping-tdd-code-reviews-57887064c412

- https://medium.freecodecamp.org/test-driven-development-i-hated-it-now-i-cant-live-without-it-4a10b7ce7ed6

## Examples

- axtreme programming - https://xtrem-tdd.netlify.app/
	- youtube example - https://youtu.be/yxO7YHkB83I
- trip service https://github.com/sandromancuso/trip-service-kata
- Example https://www.youtube.com/watch?v=QXo8bCv1BiQ
- Example https://www.youtube.com/watch?v=HRxjvaKu-X4
- Example https://www.youtube.com/watch?v=2Ekty7t621k&t=333s
- Fizzbuzz https://www.youtube.com/watch?v=NDikuKeYATg
- Fizzbuzz and refactoring to chain of responsibility pattern https://www.youtube.com/watch?v=9RJyI1Mu4wI
- palindrome https://www.youtube.com/watch?v=O-ZT_dtlrR0&t=85s
- - string calculator https://www.youtube.com/watch?v=5rADTdrjhMY
