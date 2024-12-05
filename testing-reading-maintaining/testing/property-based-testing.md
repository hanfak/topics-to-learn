# Property based testing

- See pragmatic programmer book
- A form of testing that is similar to table tests, but more flexible with random values which can be set within bounds, that tests the code.
- Focused on testing the contracts and invariants
  - what must be true, what must not be changed
  - removing edge cases and highlighting functions that leave data in an inconsistent state

## Issues

- Hard to pinpoint where the problem occured, what test case broke the test.
- Problems with setup, if unit testing, the controlling dependencies might be an issue.
  - Will need to be very tight in terms of the test cases for each set of behaviour
- USe of random values. Big issue, as a test may fail once, the pass again, lead to flakiness
  - Instead, find the test case, and values that caused the failure, and write a specific test for this, thus acting as a regression
