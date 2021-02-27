# Functional Looping

- What we generally want to accomplish in a loop
  - Mapping an array of one type into an array of another type.
  - Filtering by finding all the items in an array satisfying some predicate.
  - Determining whether any or none of the items in an array satisfy some predicate.
  - Accumulating a count, sum or some other kind of cumulative result from an array.
  - Sorting the elements of an array into a particular order.
- These operations can all be done using functional style over an imperative style (for/while)
  - Thus becomes declarative and readable, no mutating, tmp variables, no creating a collection and adding to it
  - Focus on the real work, rather than the house keeping
- Functional style allows you to chain operations together
    - imperative, will lead to multiple loops, or composed loops
- Implementing functional style might be unusual, so implement in imperative than refactor to functional
- Just cause something can be writing in a functional style does not mean it is the only way or the best way to do it
  - Functional iteration, should be a go to, if the language or a library allows it
  - imperative style only if readablity or performance is necessary or can only do it imperatively
