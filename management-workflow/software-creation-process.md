# How to do a story

Here is a way of dev completing stories. It is not one striaght through process but iterative.

- Pick story from backlog, only if it ready and team is within WIP limit

- Researching story
  - Similar stories - look for tests, look for code
  - Making notes for kickoff

- Kick off
  - https://www.agilealliance.org/glossary/three-amigos
  - gather stakeholder (ba/testers/ others)
  - Discuss Stories
  - Make notes
    - What is expected, tests to be documented
    - Answer any queries from the questions from research
    - Areas that will be affected (DB/performance testing/other apps etc)
    - Deadlines

- Story Champion
  - Some one who sticks with story from the beginning to the end (or there for the longest)
  - Point of contact for BA/testers


- TODOs in jira
  - What needs to be done
  - In table format, two columns: action and done.
  - When done put tick, or put messsage/action taken, or waiting

- Notes in jira
  - Any notes relatign to the story
  - any correspondence with stakeholders, that is relevant
  - files (patches, documentations, examples of api etc)
  - Anything in code that might affect the story (Current behaviour or issues with future behaviour)

- Development

  - ATDD and TDD
    - Start with acceptance test
      - Look for similar tests, or methods already created
    - When going into classes, doing more complex flows need to TDD
    - Check that wording of acceptance test is good, everything is logged correctly, notes added (story numbers, links to other tests)
    - Look to break tests
    - Refactor prod and test code, make code better for next user or to be able to do the story
    - Debug when test fails, then solve

  - Using diagrams

  - pairing

  - Comms with BA
    - Throughout developing the story, there might be decisions that need to be approved by the BA

  - Add and complete todos in code
    - instead of getting side tracked, look to write todo comments
      - mentioning story number ie // TODO: PHO-123 - blah blah
    - This will help stay focused on passing the test or refactoring

  - Other projects that need to change, used as libraries
    - use DEV-SNAPSHOT
    - inform others who might have a dependency on it

- Commiting
  - Checking changes to see if good
    - remove unneeded imports, fix styling
  - Write commit message - story, who worked on it, description of changes
  - commit on green build, fix other broken areas
  - Small logical commits

- Pushing to repository
  - Make sure CI build is running
  - monitor CI build

- Fixing builds
  - locally
  - after CI failure

- Other projects that need to change, repeat the above

- Splitting work
  - During the story, it might be larger than expected, this is when new stories should be created. If there is work that will take more than half a day, put it in another story. Stories should not last more than 3 days.

- Before signing off, start the application, and do a quick manual test to see if it is actually working
  - The end to end test should do this, but this might not be the case

- Sign off
  - What was completed, go through tests
  - Discuss with tester how to test if not routine



- Link acceptance/documentation tests to jira
- When done, all todos are done (jira/code), inform analyst to have a look
  - This may come back with changes to the tests (naming) to improve documentation or logs/req/rsp may not be correct and code changes will need to happen.
  - This may invovle discussions, as to whether it is appropriate or feasible for the story.

- When testers pick this up, then they may need help or clarification from devs who worked on the story
  - This can happen sometime after the story, so there may be a bit of context switch.
