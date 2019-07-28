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
