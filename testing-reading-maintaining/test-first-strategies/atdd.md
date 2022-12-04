# Acceptance Testing Driven Developement (ATDD)

## What

- a single acceptance test is written from the user’s perspective. It mainly focuses on satisfying the functional behavior of the system.
- This technique attempts to answer the question – Is the code working as expected?
- enhances collaboration among developers, users, and QAs with a common focus on defining the acceptance criteria
- key practices
  - Analyzing and discussing the real-world scenario
  - Deciding the acceptance criteria for those scenarios
  - Automating the acceptance test cases
  - Focusing on the development of those requirement cases
- ATDD is a process in which high-level acceptance tests are automated to fail and then developed against to create enough production code to make the acceptance test pass.

## Benefits

- Requirements are very clearly analyzed without any ambiguity
- Encourages collaboration among cross-team members
- The acceptance test serves as a guide for the entire development process

## How

- Do acceptance test, then do unit tests
  - double loop tdd
  - why acceptance test will show how system works (if testing whole system). This logic can happen anywhere in the application. Unit testing will force the logic of where this happens to one locale, or if spread about can test different classes via tdd. This will cover edge cases

## Links

- https://reqtest.com/testing-blog/tdd-and-atdd-an-overview-of-the-two-popular-methods-2/
- https://gaboesquivel.com/blog/2014/differences-between-tdd-atdd-and-bdd/

## When not to write

- http://www.methodsandtools.com/archive/altfunctesting.php

## Testers writing tests

- Normally write tests as html or wiki, and use a parser to convert and run the code. This makes it easier to write tests for non techically people, but harder to debug as a developer.
- Using a test framework, which can produce readable output for testers and business, makes it easier to work with and debug. It does mean setup is all codified. But testers and stakeholders, cannot change documentation and need coders to do it, unless they upskill.
- Avoids mainting wikis/html/files
- Can add extra information, ie logs, whats in the database, the request and responses at entry points and with dataproviders
- Developers better at writign test code than testers. Developers are more likely to produce maintainable tests then testers. Developers are also more likely to be faster.
- Reduce duplication in test code, when devs write tests
- Work together to write acceptance tests
  - Have the outline (no implementation) written before kickoff and get testers and BAs to agree.
  - Devs write the tests, and share them at the end and see if they meet the testers and BAs requirement.

### links

- https://github.com/bodar/yatspec
-

## Links

- https://leanpub.com/essential_acceptance_testing/read#leanpub-auto-reading-list
- https://youtu.be/3lmClkPKQ0k The key concept in computer science and how it relates to ATDD (Peter Gfader)
