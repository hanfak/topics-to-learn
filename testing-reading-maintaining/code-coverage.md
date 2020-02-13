# Code coverage

- [Code coverage](#code-coverage)
	- [What??](#what)
	- [Types](#types)
	- [Why?](#why)
	- [Aim for](#aim-for)
	- [Issues](#issues)


## What??

- A percentage that shows what amount of the code base covered by tests
- If doing TDD, this should be 100%
- Generally refered to by unit tests
- Some code cannot be covered by unit tests, but by integration or end to end tests
- A report can also be generated (ie html), which shows what places in the code base was not covered by the test

## Types

- Line
  - ie jacaco, intellij coverage
  - checks which lines of the code base are touched when a test is run
  - Issues
    - May not cover all logic
- mutation
  - ie pitest
  - Static analysis
  - Changes code in source, and checks if tests fails
  - Far more rigorous in checking codebase is covered by tests
  - Issues
    - For large code bases can take a long time
    - Not useful as part of CI, should be run at night (build agents are free)

## Why?

- To have confidence that codebase was tested
- No extra code was in place that should not be, ie hacked on code that coould be malicious
- When refactoring, coverage will show if it is covered by tests (ie you add extra source code)

## Aim for

- 100%
  - Libraries
- Less than sweet spot
  - Get features out fast ie startup, deadline
- More than sweet spot
  - Where nothing breaks, ie reputation counts or lots of legal laws

## Issues

- Aiming for 100%
  - Yes for libraries
  - Can be hard, a lot of effort goes into it for little business gain
- Less code coverage can lead to bugs
- With 100% coverage, your code is still relying on libraries which might not have a high coverage
- Code should by covered by unit tests only is a common theme
  - This is wrong and leads to duplicate testing (ie integration and unit test testing the same thing)
    - There can be cases for duplicate tests ie checking business rules for different cases
  - Code should be tested for behaviour not implementation
- HIGH CODE COVERAGE DOES NOT EQUAL HIGH TEST COVERAGE .
  - Just as test could pass through a piece of code, does not mean it is covered in terms of what it could do (ie it could return null or exception etc)
  - https://capgemini.github.io/testing/What-Is-Code-Coverage-and-Why-It-Should-Not-Lead-Development/
