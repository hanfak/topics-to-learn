# Approval Testing

- Golden Master Testing”, “Characterisation Testing” or “Snapshot Testing”

## What

- A way of testing code, which has no/little tests
- Can use examples given in documentation, to find the output of the code and use this as standard you code after refactoring must meet
- Finds a way of getting results of output, to form unit tests, especially useful when code is complex and undocumented.
  - This can be used to write a suite of unit tests

## When to use

- Will generally have to run all the code, so no stubs/mocks
- For methods that return some output, we store the output in some file and use this file to compare future calls
- For side affect methods, ie db/files, can get a snapshot of these changes in some format (file contents, or object) to compare with future calls
- For an app, ie webserver, can use a logger/interceptor to record the response sent back to the user
  - This includes logging all changes to database, logs, files
  - This will be heavy weight, so not great to use all the time

## why

- Helps in refactoring legacy (non tested) code
- provides safety net while refactoring when there is no test suite
- Helps create a test suite
- Finds bugs as you refactor, this leads to a discussion point with stakeholders of what to do with them
- Good for tinkering with non tested code 
  - especially if commiting

## How 

- May need to iteratively create several approval tests, so that you cover all the code paths before refactoring and adding behaviour 
  - use code coverage tools
- Do not change behaviour
  - keep bugs and have example approval test for a bug

## Issues 

- This can be a cheat way for avoid TDD or real tests, and can end up being stuck in code bases
  - should be deleted after use, and behaviour encapsulated in proper tests using a test harness
- you shouldn't use approval checks as part of integration tests, as their results change too often, and who's got time to review and approve new results?
- approval tests don't really work as proper correctness checks
- approval tests shouldn't make up the majority of your tests, far from it
- Limited scope: Approval testing only verifies that the output of the software matches the expected output for a given set of inputs. It does not verify the functionality or performance of the software beyond that.
- Manual effort: Approval testing can require manual effort to create and approve the expected output, which can be time-consuming and error-prone.
- High maintenance: Approval tests can become difficult to maintain as software changes over time. When the software changes, the expected output may need to be updated, which can be tedious and time-consuming.
- False positives: Approval testing can produce false positives if the expected output is not updated to reflect changes in the software.
- Limited applicability: Approval testing is not suitable for all types of software, particularly software that does not have deterministic output or where the output is difficult to predict.

## Libraries

- https://github.com/approvals/ApprovalTests.Java
- https://approval.readthedocs.io/en/latest/getting-started.html
- https://approvaltests.com/
- https://www.softwaretestingmagazine.com/knowledge/approval-testing/

## Links 
- https://youtu.be/jAMVtMesHqk Continuous Delivery - What Is Approval Testing?
