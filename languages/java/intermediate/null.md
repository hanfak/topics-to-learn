# Null

- https://stackoverflow.com/questions/2707322/what-is-null-in-java

## what it means

- Value was never initialized (whether accidentally or on purpose)
- Value is not valid
- Value is not needed
- No such value exists
- Something went terribly wrong and something that should be there is not

## Alternative

- Use Optional.empty()
  - Example, ask the database for a Customer with a given ID. Previously, you might have used null to represent this, but that could be ambiguous – does it mean the customer wasn’t found? Or that there’s a customer with that ID, but has no values? Or was null returned because the connection to the database failed? By returning an empty Optional, you’ve removed the ambiguity – there’s no customer with that ID.
  - Not a solution to everywhere you find a null.  But if a method is deliberately returning a null value to mean “not found” or “I don’t have one of those”, this is a good candidate for returning an Optional.
- use of final fields, so objects are alwasy initialized in constructors
- Use of builders and factories to validate correct combinations before instantiation
- not using nulls in the core of your application (i.e. pushing all checks to the edges)
- @NotNull/@Nullable.
  - One of the problems with complex code bases is understanding what are actually valid values. If you’re checking for null parameters, try putting @NotNull on the signature and seeing if null values are ever passed.  If nulls are never passed, you can remove the null check.

## Code smell

- Leads to lots of null checks
  - If application is well designed, and we are incharge  of what gets passed to an object, we can avoid null checks as we know that null will never get passed to an object (constructor or method)
- nulls could mean lots of things
- Exception handling. Returning null for an Exceptional case is very unfriendly, and unexpected from the caller’s point of view.  It can lead to NullPointerException further down the line, or at least more of the pervasive null checks (without a clear idea of why the value is null).  Throwing a descriptive Exception is much more valuable for those downstream.
