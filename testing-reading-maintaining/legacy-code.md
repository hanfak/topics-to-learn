# Legacy code

Many different definitions (See links), but mainly about code that is made sometime ago by developers who are no longer around, using technologies/libraries which are outdated or not supported, and probably written with bad structure, poor or little testing, poorly engineered. But they are still used by the business and need to be maintained, thus making it hard to do so.

## Write tests before refactoring

- Have a 100% coverage of the required behaviour before changing anything.
- Test from smallest to largest/deepest branch
- Called Charactisation Tests
- Need to understand the code first
  - This can be hard, so use IDE to do some simple refactorings (change name, extract method) to make code easy to understand to be able to write the tests

### Write seams to handle hardcoded dependencies

- Singletons, static methods or instantiated objects in the class under test makes testing hard
- An intermediate step is to create an subclass of class under test, where the hard coded dependencies in prod code are moved to a protected method, thus the sub class can override them with stubbed out responses to match the test cases
- overload the constructor, where original constructor will new up the object, and the main constructor can have a param for that newed object, and thus inject a stub/mock in.

## Signs of hard to test code

- http://misko.hevery.com/2008/07/30/top-10-things-which-make-your-code-hard-to-test/

### When fully covered by tests refactor

- Refactor from deepest to shortest branch
- Before refactoring, need to understand why the method/block is so big?
  - Does too much
  - Need to ask, does this behaviour belong here?
  - Can spot "feature envy", where the class is using too much of the information from another class (it's dependency, argument), when that other class could just give it to the class under inspection

## Golden Master

- Is technique to use when refactoring (and/or testing) legacy code
- If dont know what is going on
- If working with multiple classes, use approval testing (have original results of golden master in a file and thus new changes can be places in a new file and comparisons can occur)
- Gives us confidence that the system works with examples that we now to be true
  - These examples can be found from production data (ie logs)
  - Can inject a service virtulisatoin system in between caller and callee, to record the req/resp
  - Could ask business logic, documentation for the cases or business rules
  - Can inject logs that show what inputs and ouputs and interactoins take place (blocks reacher), but only for short time to reduce log memory piling up
    - this can be used, if there is an effective manual or outside testing that occurs
- If no way of getting the truth of what it does, can use random inputs
- The golden master is:
  -  set of x random inputs
  -  bombard the system/class/module under test with these inputs
  -  capture these outputs or side effects, some file
  -  when the changes are made to SUT the golden master is run with the results compared with the original results, to make sure nothing is broken
  -  When all tests are green (old and new match), then can add unit tests as you refactor
-  Altenative way, only good if changing one test at a time, unfeasibly for multiple classes or testing the whole system
  - Keep the original class under test and work on the duplicate
  - run the same golden master tests/inputs on both classes
  - Compare results of both,
-  Use of approval testing libraries
-  Problems
  -  If no ouput, will need to add logs to the code.
    -  but when finished, should have a set of tests that document behaviour and can remove logs
  - non-deterministic output
    - Solution: The solution for this is taking control of the random number generator and seeding it with the same numbers every time.
  - If the code under test is too complex to generate templates for every possible input, you have to use sampling.
  - Noisy output
    - Will need to filter it out



### Links

- https://www.codurance.com/publications/2012/11/11/testing-legacy-code-with-golden-master
- example https://www.youtube.com/watch?v=cI7CtKwsE_w
  - https://github.com/Morinslash/GildedRose-MeetUp
- https://blog.thecodewhisperer.com/permalink/surviving-legacy-code-with-golden-master-and-sampling
- https://blog.thecodewhisperer.com/permalink/how-not-to-write-golden-master-tests
- https://blexin.com/en/blog-en/golden-master-pattern-dont-fear-the-legacy-code/

## Start from scratch

- Good if SUT is simple and business rules are known
- Being with a new class, and build the implementation using TDD, then replace the old class with it (wire it in) as long as it does exactly what the old class did
- Can use a golden master as a check when code has been implemented
## Links

- https://en.wikipedia.org/wiki/Legacy_code
- https://www.techopedia.com/definition/25326/legacy-code
- https://www.quora.com/What-is-legacy-code
- https://www.quora.com/What-is-your-definition-of-legacy-code
- https://softwareengineering.stackexchange.com/questions/94007/when-is-code-legacy
- sandro manscu live example https://www.youtube.com/watch?v=_NnElPO5BU0
- https://www.codurance.com/publications/2011/07/03/working-with-legacy-code

## Books

- [working with legacy code - feathers]()
