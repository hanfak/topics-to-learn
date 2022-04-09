# Legacy Code

## What?

- Many different definitions (See links)
  - but mainly about code that is made sometime ago by developers who are no longer around,
  - using technologies/libraries which are outdated or not supported,
  - and probably written with bad structure,
  - poor or little testing,
  - poorly engineered
  - not kept upto date
  - Code that predates current team
  - that has not been touched in living memory
  - But they are still used by the business and need to be maintained, thus making it hard to do so.

- Legacy Code is valuable code you’re afraid to change.
  - Without tests, makes it hard to change without knowing if something has broken
      - code without tests is tricky to change without introducing a regression somewhere.
    - But Code with tests can also be Legacy Code
      - Poorly written tests can get in the way
        - ie Only there for test coverage, doing too much, hard to understand
    - Also some code bases, or parts/modules may not have test but easy to change
      - Much rarer
  - Better definition is valuable code you're afraid to change
    - For example, searching for a bug and making a change to fix it
    - Contributing factors:
      - Unfamiliarity with the code plays a lot
        -  We overestimate the complexity of unfamiliar code.
        - Not working on the code base recently or changing context from another codebase/domain can affect remembering how it works or navigating it
      - Good tests make you comfortable changing unfamiliar code
      - It gets better after a few months.
        - Time spent working on it, improves ability to work with it
        - The way you feel about it, becomes less dread and more acceptance
      - Most of the code is terrible
        - At the time it might have been good, but it rot sets in

https://understandlegacycode.com/all-articles/

## Reasons for dealing with legacy code

- It's legacy cause it works and does not need to changed (Rarely does), but there are cases when it does
- It needs to change
  - internal reasons
    - New features
    - new bugs
  - external reasons
    - ports to new hardware or operating systems
    - new versions of dependencies, language
    - security, vulnerabilities
    - new laws
    - new versions of api
    - api being decomissioned
    -
