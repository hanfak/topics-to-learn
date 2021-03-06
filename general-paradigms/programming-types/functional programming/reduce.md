# Reduce

- It is a terminal operation on a data structure
  - returns a single value
- other names
  - fold
  - aggregate
- The reduce method takes two arguments, which are:
  - An identity value (1) and the default result if the data structure is empty
  - A lambda that is executed for every element in the stream and itself takes two arguments:
    - One argument receives the value of current stream element.
    - The other receives the identity value on the first iteration, and on every subsequent iteration it receives the result of the previous computation.
  - The final result of the reduce method is the result of the lambda function on the last element in the stream.
- Whatever the identity value is, it must satisfy the condition that when it is passed to the accumulator function along with any other value, the other value is returned as the result.
- Examples of reduce (prebuilt methods in language)
  - collecting to a data structure (list, map)
    - GroupingBy
      - for grouping objects by some property and storing results in a Map
  - You can reduce an array of one type of elements down to a result of a completely different type
    - count
    - sum
    - join to make a string
  - Matching
    - check if something or all matches some predicate
      - allMatch
      - noneMatch
      - anyMatch
    - Find all elements which match some predicate
      - findall
      - FindFirst
      - findOne
  - getting a particular item by some metric
    - max
    - min
