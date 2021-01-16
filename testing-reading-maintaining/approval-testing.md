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

## Libraries

- https://github.com/approvals/ApprovalTests.Java
- https://approval.readthedocs.io/en/latest/getting-started.html
- https://approvaltests.com/
- https://www.softwaretestingmagazine.com/knowledge/approval-testing/
