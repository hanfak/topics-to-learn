# Functional Programming

- AKA Declarative Programming
- Intent of FP is for readability and understandablility
- About what rather than how (procedural)
- functional programming as a paradigm begins with three things, the three main concepts — actions, calculations, and data. These are mutually exclusive categories that everything falls into.
- Functional programming, therefore, is programming so as to avoid these side effects wherever possible.
- Functional programming imposes discipline on mutating state.
- A functional language makes all data immutable by default.
- FP makes code understandable by minimizing moving parts (mutating state).

## Types

- https://functional.works-hub.com/learn/Where-did-the-Functional-Languages-come-from-
  - Clojure
  - Erlang
  - Haskell
  - OCaml
  - F# (hybrid)
  - Scala (hybrid)
- https://functional.works-hub.com/learn/On-Types-And-Intent

## Properties

- Pure functions
- functional composition
- lazy evaluation
- High order functions
- Immutability

## Pure functions

- No side effects
  - avoidance of changing state
- Only acts on the inputs
- Always returns the same outputs regardless the number of times called
- idempotent
- do not depend on anything that could change or have side effects
- the output value of a function depends only on the arguments that are passed to the function, so calling a function f twice with the same value for an argument x produces the same result f(x) each time.
  - impure functions
    - they depend on state that may change outside the function. This external state might be in the form of global variables, or objects, it might be in a file, or a database, or any number of other thing
    - These are side effects
  - Pure functions element side effects

### side effects

- Statements
  - assign a variable, reassign a variable, call a procedure, etc.
  -  Statements cause side effects.
-  Functional programming takes this idea further, and asserts that it is better not even to modify local, private variables.

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

## Properties

-

## Drawbacks of functional programming

- https://alvinalexander.com/scala/fp-book/disadvantages-of-functional-programming
- https://www.quora.com/What-is-the-dark-side-of-functional-programming-What-problems-are-not-suited-for-functional-programming-What-problems-arise-in-large-deployments

## Glossary

- https://github.com/hemanth/functional-programming-jargon

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
- https://completedeveloperpodcast.com/episode-75/
- https://github.com/leandrotk/functional-programming-learning-path
- https://functional.works-hub.com/learn/an-introduction-to-the-basic-principles-of-functional-programming-f509c
