# Map

- An intermediary operation
- it keeps all the elements
  -  the cardinalty of inputs/domain equals the cardinality of outputs/range
- similar to the data structure (objects that store key value pairs)
  - it is a noun
- One set of things is being mapped to a differnt set of things
- It is a verb
  - a function maps an array of values to another array of values.
- Say you have a function f and an array of values A = [a1, a2, a3, a4]. To map f over A means applying f to every element in A:
  - a1 → f (a1) = a1’
  - a2 → f (a2) = a2’
  - a3 → f (a3) = a3’
  - a4 → f (a4) = a4’
  - then assembling an array of the results in the same order as the inputs:
    - A’ = map( f, A ) = [a1’, a2’, a3’, a4’]
-  A way of removing loops
  -  use of streams in java and fluent interfaces to implement actions on elements in a data structure

# Flatmap

- It is doing two opertaions
  - flatten
    - turn array of array into one array
  - map
