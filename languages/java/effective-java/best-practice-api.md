#Best Practices for api

## Free up resources in reverse order 

- **Whenever you implement logic using before/after, allocate/free, take/return semantics, think about whether the after/free/return operation should perform stuff in the inverse order.**
- similar to destructors in c++
- For example
  - When using @Before and @After JUnit annotations
  - When allocating, freeing JDBC resources
  - When calling super methods
- https://stackoverflow.com/questions/8274098/possibility-of-starvation-of-dining-philosophers

## Don’t trust your early SPI evolution judgement

- Service provider interface (SPI) is an API intended to be implemented or extended by a third party
  - Providing an SPI to your consumers is an easy way to allow them to inject custom behaviour into your library / code
- Creating an SPI,  may trick you into thinking that you’re (not) going to need that additional parameter.
- once you’ve published your SPI and once you’ve decided following semantic versioning, you’ll really regret having added a silly, one-argument method to your SPI when you realise that you might need another argument in some cases
  - YAGNI
- API evolution will prevent you from adding that parameter easily
- better than polluting your SPI with dozens of methods, use a context object (or argument object)
  - Can define a type, but can keep adding data to the context object without breaking the interface
- **Whenever you specify an SPI, consider using context / parameter objects instead of writing methods with a fixed amount of parameters.**
- **good idea to also communicate results through a dedicated MessageResult type, which can be constructed through a builder API.**

## Avoid returning anonymous, local, or inner classes

- They keep a reference to the outer instance. And they will drag that outer instance to wherevery they go, e.g. to some scope outside of your local class if you’re not careful.
  - This can be a major source for memory leaks, as your whole object graph will suddenly entangle in subtle ways.
- **Whenever you write an anonymous, local or inner class, check if you can make it static or even a regular top-level class. Avoid returning anonymous, local or inner class instances from methods to the outside scope.**
- Avoid double-curly braces for simple object instantiation
  - ie for hashmap init
  - leverages Java’s instance initializer as specified by the JLS §8.6.
  - This now keeps a reference to the outer instance, whatever that just happens to be

## Use functional interfaces 

- or SAM (single abstract methods )
- Consumers like them 
- The best SAMs are those with single arguments, as they will further simplify writing of a lambda

## Avoid returning null from API methods

- Help reduce number of NPE
- This allows users to chain methods
- return iterable objects or optional
- nulls can happen with lazy init
  - lazy initialisation should be used carefully, only.
  - ie If large data structures are involved.

## Never return null arrays or lists from API methods

- always instantiate a list 
- reduce null checks
- use empty arrays or collections

## Avoid state, be functional

- Like http protocol 
- pass in data to method
- It is very hard to correctly deal with stateful APIs in multi-threaded environments
- It is very hard to make stateful resources globally available, as the state is not documented
- **Manipulate less object state.**
  - Like jdbc 

##  Short-circuit equals()

- In large object graphs, you can gain significantly in terms of performance, if all your objects’ equals() methods dirt-cheaply compare for identity first:
- apply  null checks first

##  Try to make methods final by default

- if you’re in full control of all source code, there’s absolutely nothing wrong with making methods final by default
  - If you do need to override a method (do you really?), you can still remove the final keyword
  - You will never accidentally override any method anymore
- This specifically applies for static methods, where “overriding” (actually, shadowing) hardly ever makes sense
  - static methods don’t override each other, as the call-site binds a static method invocation at compile-time. If you’re unlucky, you might just get the wrong method accidentally.

##  Avoid the method(T…) signature

- Using `Object.. all` argument type is fine 
- But is differetn `T... all`
  - T can always be inferred to Object.
  - You cannot overload, as makes it ambiguous
    - you will never again be able to typesafely overload it.
  - 