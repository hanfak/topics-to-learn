# Clean Code

# Notes

- https://github.com/jbarroso/clean-code
- https://github.com/JuanCrg90/Clean-Code-Notes
- https://gist.github.com/wojteklu/73c6914cc446146b8b533c0988cf8d29
- https://www.planetgeek.ch/wp-content/uploads/2013/06/Clean-Code-V2.2.pdf
- https://monami555.github.io/2016/01/13/clean-code-robert-c-martin-notes.html#12-concurrency
- https://www.youtube.com/watch?v=QiaDztJZO5Q
- https://youtu.be/6va1hAyh-M8 DevTernity 2021: Victor Rentea – Clean Code, Two Decades Later

# Types

- Avoid unnecessary comparisons
  - Dont compare against boolean
- Avoid negations
  - in conditionals
- Return boolean from statement, rather than using if statement
- Simplify boolean expressions
  - extract to methods with meaningful names
- Avoid null pointer exceptions in conditionals
  - check for null onf arguments before checks for domain specific illegal values, check for common default values then specific values
- Avoid switch fallthrough
  - use break at the end of each case
  - use default to catch call
- Always use braces with if/else
- Ensure code symmetry
  - Keep all branches in if/else the same, seperate different to seperate if block
- Replace magic numbers with constants
- Favour enums over integer constants
- For-each over for loops
- Avoid collection modification during iteration
- Avoid compute intense operations during iteration
- Group with new lines
- Favour string format over concat
- Favour Java API over DIY API
- Use java naming conventions
- Avoid single letter names and abbreivations
- Fail fast
- Always catch most specific exceptions
- In exceptions, explain cause in the message
- In exception show the stack trace
- Always check type before casting
- Always close resources
- Explain Empty Catch
- Structure Tests Into Given-When-Then
- Use Meaningful Assertions
- Use Reasonable Tolerance Values
- Let JUnit Handle Exceptions
- Describe Your Tests
- Favor Standalone Tests
- Parametrize Your Tests
- Cover the Edge Cases
- Split Method with Boolean Parameters
- Split Method with Optional Parameters
- Favor Abstract Over Concrete Types
- Favor Immutable Over Mutable State
- Combine State and Behavior
- Avoid Leaking References
- Avoid Returning Null
- Favor Lambdas Over Anonymous Classes
- Favor Functional Over Imperative Style
- Favor Method References Over Lambdas
- Avoid Side Effects
- Use Collect for Terminating Complex Streams
- Avoid Exceptions in Streams
- Favor Optional Over Null
- Avoid Optional Fields or Parameters
- Use Optionals as Streams
