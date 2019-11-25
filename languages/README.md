# Languages 

## What are programs

- Programs exist to make decision
- To automate repeatable actions

## Aims of learning a language

-  When you first learn a language, your job is to learn how to use it to do the jobs you already know how to do.

## properties

- Interpreted means the code is executed by an interpreter rather than a compiler.
- Compiled
-  Dynamically typed means that types are bound at execution time rather than compile time.
  - Dont need to declare variable, method types
  - There are disadvantages: you can’t catch as many errors as you can with static typing because compilers and tools can catch more errors with a statically typed system.
- Statically typed
- Strongly typed languages check types for certain operations and check the types before you can do any damage.
  - This check can happen when you present the code to an interpreter or a compiler or when you execute it
- Trade off between dynamically interpreted and statically compiled
  - flexibility versus execution safety
- Object-oriented means the language supports
  - encapsulation (data and behavior are packaged together),
  - inheritance through classes (object types are organized in a class tree),
  - polymorphism (objects can take many forms).
  - The whole premise of the model depends on wrapping behavior around state, and usually the state can be changed. This programming strategy leads to serious problems with concurrency.
- Look for syntactic sugar, those little features that break the basic rules of the language to give programmers a little friendlier experience and make the code a little easier to understand.
- Some languages are OO but have procedural elements
  - like java, where int a = 4; is not an object, it is a primitive. It does not have behaviour ie a.add(5); but have 4 + 5;
- Prototype languages like Io, Lua, javascript and Self use the object, not the class, as the basis for object definition and even inheritance.
  - every object is a clone of an existing object rather than a class
- Duck typing doesn’t care what the underlying type might be. If it walks like a duck and quacks like a duck, it’s a duck.
  - the idea of to code to interfaces rather than implementations
  - ie Ruby
  - Static typing allows a whole range of tools that make it easier to do syntax trees and thus provide integrated development environments.
    - poor debugging
- Mixins
  - interface
- Metaprogramming
  - programming that programs itslefs
  - reflection
  - change classes onthe fly
