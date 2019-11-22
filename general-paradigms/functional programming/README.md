# Functional Programming

- AKA Declarative Programming
- Intent of FP is for readability and understandablility
- About what rather than how (procedural)

## Pure functions

- No side effects
- Only acts on the inputs

## Immutability

## When not to use

- When the code becomes
  - messy (greater than one line lambdas )
  - lots of exit points (ie exceptions)
- When there are side effects
  - ie dealing with external input like database, io etc
  - A purely functional program, cannot take any outside input, cannot really do anything
- Use of forEach()
  - takes a consumer, which has side effects
  - `s -> {}` is a pure consumer, but does nothing and useless
- Alternative to consumer, is a supplier
  - does not take any input and returns a value

## Advantages

- https://alvinalexander.com/scala/fp-book/benefits-of-functional-programming
- https://itnext.io/pros-and-cons-of-functional-programming-32cdf527e1c2

## Drawbacks of functional programming

- https://alvinalexander.com/scala/fp-book/disadvantages-of-functional-programming
- https://www.quora.com/What-is-the-dark-side-of-functional-programming-What-problems-are-not-suited-for-functional-programming-What-problems-arise-in-large-deployments

## Links

- https://dev.to/riccardo_cardin/object-oriented-programming-strikes-back
- [The Three Paradigms - Uncle Bob](https://blog.cleancoder.com/uncle-bob/2012/12/19/Three-Paradigms.html)
- [FP vs OO](https://blog.cleancoder.com/uncle-bob/2018/04/13/FPvsOO.html)
- https://dzone.com/articles/when-functional-programming-isnt
- https://dzone.com/articles/functional-programming-principles-every-imperative
- https://github.com/hemanth/functional-programming-jargon
- https://codurance.com/2018/08/09/the-functional-style-part-1/
- https://blog.knoldus.com/functional-programming-a-paradigm/
- https://github.com/blalasaadri/functional-programming-in-java-examples
