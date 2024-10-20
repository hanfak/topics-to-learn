# Yatspec

## What?

- An BDD acceptance test framework
- An extension of junit

## Aims:

- As a secondary memory for analysts to use
  - A form of easily readable documentation
- Testers, easier to write
- For devs, faster, encapsulation, ease of refactoring
- increase communciatoin betwee dev/qa/ba
- log don specify


## Why?

- why dev writes the test, compared to BA or QA?
  - Feedback loop is quick
    - dev wrote the test, it breaks, the dev fixes it immediately
      - frees time of QA to do testing
      - Can push completed tests, have the output given to tester/ba mid story and they can check if it makes sense or is feasible
      - Allows tester to work with app (create support tools for qa) so they check that yatspec test work
        - rather than before, they would only interact with app via html/feature files
    - otherwise, feedback loop is longer, as tester/ba has to check it, and then it comes back to dev
      - how can tester fix the test, cause they did not write the layer that runs the test with the html or the prod code
- Maintance is easier
- Code becomes better engineered, easier and faster to create tests and debug failing tests
  - Can create a builders and DSL for creating tests
- it generates the sentences of the acceptance tests from the code, making it easy to keep test code and html output in sync.
- how the output logs nicely all the interactions in the system, providing a low-level documentation of the API for the application.
- Better output
  - Can show and highlight primed state
  - Can show req/resp with app and services
  - Can show state of database before and after execution of flow
  - Can show a sequence diagram of the flow
  - Text of test is transformed into custom readable doucment
  - Can link between other tests
  - Can add notes to add more documentation
  - Can add links to jira stories
  - Add screenshots to documentation. Makes testing UI easier
  - searchable index
- Can work with business to create tests that satisfy their desires
- Log dont specify
  - output shows specifics which are tested, everything else is logged for user to see in html output
  - Only assert on key things required for the flow
  - Only prime the key things needed for flow to occur
    - everything else is defaulted
  - No full flow of several usecases to get to primed state
- Enforces domain langauge in code, and that used by ba
  - Makes code more readable and understandable
- Testers can create them if they know some basic java, or show them how to implement your builders for them
- Coders dont have to write in a specific format (ie html/features)

## Issues with alternatives

- Brittle tests
- Easy to write bad plumbing/fixtures (this needs tests)
  - need to engineer this, more time than needed spent on test rather than prod
- NEed to learn a DSL, and it's magic when things go wrong
  - hard to debug or rather not obvious
- Concordian
  - Can lead to overspecifying, which leads to a change in some area affecting tests which doesnt test the changes made
  - Devs/QA having to rewrite the html, when the specs given do not match up
    - This can be error prone, people dont like it
    - Duplicated effort
  - A lot duplication

- Cucumber/gherkin
  - adds another layer of complexity
  - Writing generic enough functions, which can interept the document created by the analysts, to be used for different scenarios
    - Need to check that all previous functions can be used
  - This does reduce the amount of teamwork possible. Because the steps written by the analyst might require some change to be specific enough or to be generic enough to be reused
    - And we cannot expect someone not dedicated to the testing framework, to know all currently available steps. Or how the code behind the step works. So now, an analyst is advising steps rather than providing them. Meaning that in the end, steps might have to be changed or discarded.



## Links

- http://javing.blogspot.com/2015/12/using-pictures-in-your-acceptance-tests.html
- http://javing.blogspot.com/2015/03/yet-another-blog-article-about.html
- https://github.com/bodar/yatspec
- https://codeforfunandmoney.wordpress.com/
- https://medium.com/ft-product-technology/behaviour-driven-development-at-the-ft-46dc2991471d
- https://vimeo.com/17846934

## Alternative 

- https://gitlab.com/kensa/kensa



Anything longer than two hours is taking people for granted. Our test, a simple custom oop kata with some boiler plate for them to finish, which we now only use with contractors (permies are giving a 30min tech screen, but all candidates do a pair test) are a max of 2 hours which is stated on the instructions. If they are good, and the amount we pay them they should be, they should crack it out in an hour with tests and well designed, for comparisons our mids can crack it out in less than 2 hours. 

I think giving someone a whole range of requirements (which would be a story each) and start from scratch, and especially if you need to do a webserver, I would say no, cause this will take ages for possibly little reward.

Bigger issue is the marking, the big the solution, the longer it takes to mark (or it becomes like code reviewers checking massive pull requests  compared to smaller ones). We get it down to around max 10-15 minutes each test, and two people have to do it. The majority failed tests, can be marked in 2 mins. Approx 60+% dont pass this first stage, so we dont waste time doing the pair test. So the cost is not worth it for the company, so why bother set such a convoluted test to waste your developers time?

I think these places with long tests, dont know what they are looking for, and just try something and dont really evaluate it (Agile) 