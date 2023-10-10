# Optional

- Monad

## why

- To get compile time exceptions rather than runtime exceptions
  - get feed back faster
- when you return something that may or may not exist

## When not to use

- When return a collection, use empty list or the collection
- when the return value is always going to exist
- As a parameter
  - will need to do an `ifPresent` check and pass in the optional
  - use two separate methods (overloading), one with no param and another with the param

## Links

- https://youtu.be/Ej0sss6cq14?si=89GPkgKS92zlXaMt Optional - The Mother of All Bikesheds by Stuart Marks

