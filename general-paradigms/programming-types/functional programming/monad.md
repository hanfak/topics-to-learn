# Monad

-  is a design pattern
  -  The Monad pattern defines what it means to chain operations together, enabling the programmer to build pipelines that process data in a series of steps,
-  a Monad wraps a typed value (of any type) and maintains some additional state separately from the wrapped value.
  -  In the case of the Optional monad, the additional state is whether or not the value is present.
  -  the MaybeValid monad, it is whether or not the value is valid, plus a validation error in the case that it is not.
-  In functional programming, a monad is a structure that represents computations defined as sequences of steps. A type with a monad structure defines what it means to chain operations, or nest functions of that type together.
-  More formally, the monad pattern is usually defined as an assemblage of the following three components, which together are known as a Kleisli triple:
  -  A type constructor that maps every possible type to its corresponding monadic type. This wording does not make much sense in Java. To understand it, think of generic types, e.g: Isbn → MaybeValid<Isbn>.
  - A unit function that wraps a value in an underlying type with an instance of the corresponding monadic type, e.g: new Valid<Isbn>(isbn).
  - A binding operation that takes a function and applies it to the underlying type. The function returns a new monadic type, which becomes the return value of the binding operation, e.g: map(book -> new SingleBookResult(book)) which yields a MaybeValid<SingleBookResult>.
- ie
  - Optionals
    - Maybe it is or isnt
  - Either
    - Maybe it's this or something else (or exception)
- You can supply the Monad with a function that operates on the wrapped value. Whatever the type is of the wrapped value, the function's argument must match it. The Monad will pass its wrapped value to the function and will yield a new Monad, of the same monadic type, encapsulating the value returned by function.
  - “binding operation
  - The wrapped type of the new Monad may be different and that is fine.
  - If there is some functionality associated with the Monad's additional state, the Monad handles it as part of the binding operation
    - when you pass a function to an empty Optional, the function will not executed; the result is another empty Optional.
  - you can call a chain of composed functions in sequence, morphing from type to type, all within the context of the Monad.
- the Monad provides a means for you to handle the value, taking account of the additional monadic state, in whatever the appropriate manner is given the context of your program
- the Monad provides another tool in your box for creating abstractions, helping you to reduce the global complexity of your programs.

## Links

- https://stackoverflow.com/questions/2704652/monad-in-plain-english-for-the-oop-programmer-with-no-fp-background
- https://ericlippert.com/category/monads
- https://medium.com/polarizertech/refactoring-if-else-either-and-flatmap-4f1ca9076664
