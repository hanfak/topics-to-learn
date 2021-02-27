# Refactoring

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Refactoring](#refactoring)
	- [aims](#aims)
	- [Slicing big functions](#slicing-big-functions)
		- [Extract for loops](#extract-for-loops)
		- [Extract intensive uses of the same object](#extract-intensive-uses-of-the-same-object)
		- [Raise the level of abstraction in unbalanced if statements](#raise-the-level-of-abstraction-in-unbalanced-if-statements)
		- [Lump up pieces of data that stick together](#lump-up-pieces-of-data-that-stick-together)
		- [Follow the hints in the layout of the code](#follow-the-hints-in-the-layout-of-the-code)
	- [Slicing big objects](#slicing-big-objects)
	- [Better naming](#better-naming)
	- [Remove duplication](#remove-duplication)
	- [nested if statements](#nested-if-statements)
	- [Making side effects visible](#making-side-effects-visible)
	- [Conditional to polymorphism](#conditional-to-polymorphism)
	- [replace method with method object](#replace-method-with-method-object)
	- [Links](#links)
	- [Book](#book)

<!-- /TOC -->

- Generally part of TDD cycle
- Cannot refactor everything, bit by bit
  - When working on new feature, or fixing bugs
- Can do massive refactors if necessary, due tech debt getting out of control.

- use of IDE to refactor
  - shortcuts
  - looking for yellow warnings

- https://martinfowler.com/articles/workflowsOfRefactoring/#final
- https://completedeveloperpodcast.com/episode-27/

## aims

- The point of a refactoring is to improve the quality of a region of the code.
  - We should write good code because it helps the business.
  - Good code leads to less bugs, faster integration of new features, less employee turnover in the company
- refactoring a piece of code that doesn’t pose a problem (direct or indirect) to the business is a waste of time, energy, and money
  - the business doesn’t know which refactoring will bring them value, because they don’t know the state of the code as much as you do
- a region of code that corresponds to an unstable feature that has a lot of bugs is a great candidate for refactoring
- valuable refactorings are those that will let you do your job more efficiently.
- should refrain from investing time in the refactoring projects that have a low value/cost ratio.
- little point in refactoring code that you don’t interact with often.
- don’t do a refactoring just because it is cheap

- https://stackoverflow.com/questions/498651/goals-of-refactoring

## Slicing big functions

- End up this way due to laziness
- Can have too many responsibilities, or too many implementation details about it's responsibility
- Need to identify the units of behaviour in function
- split into sub functions of delegate to another object
  - decide if it is the initial function that should call them, or another part of the code
  - Rename correctly
    - The function’s name should reflect what the code does and not how it does it.
- Issues
  - Adds another layer of indirection
    - makes it hard to follow - going back and forth
  - If performance is hit, can use a profiler, and the break down of functions allows to  better pinpoint bottle neck

### Extract for loops

- A for loop often represents a unit of behaviour in a long function
- Categories
  - the loops that perform an algorithm (search, sort, etc.)
    - use an existing implementation of this algorithm
      - library
      - especially for common/standard algorithms
  - the loops that do a simple iteration on a collection and perform the same treatment to each element
    - split parts of it
    - issues with nested for loops
      - may want to show the nesting to show complexity

### Extract intensive uses of the same object

- understand the number count of objects used and the span within the function
  - the proportion that span takes in the length of the function. This proportion is the span divided by the total number of lines of the function, and can be expressed as a percentage.
- The words with a high number of occurrences and low proportion are good leads for identifying some of the units of behaviour of the function, to extract

### Raise the level of abstraction in unbalanced if statements

- In an if statement that has both an if branch and an else branch, we should expect the two branches to be at the same level of abstraction.
  - The bodies in the branches should either deal in abstractions or implementation not having a mix of both
- Look for branches with differing lengths
  - need to check the abstraction level and see if it can be extracted
- Error cases
  - throwing exception in one branch
  - Not a problem, the other branch can be more detailed
  - Can use guards (short if statements at the beginning of the function)
    - to separate the code of the error cases from the main code
    - Exception is dealt with before doing the main action

### Lump up pieces of data that stick together

- Some functions get very long because they contain repetitions of the same pattern over and over
  - Wrapping that pattern in a function or object, and using that wrapper each time instead of writing the whole pattern
- ie value and currency always being called, assigned or used together, better to extract to object like Amount and use this
- Pieces of data that are always manipulated together in code don’t necessarily correspond to one unified concept, but they are good candidates for deciding if they do.

### Follow the hints in the layout of the code

- blank lines between lines of code in function, separates logical entities can be extracted
  - Or comments at start of section of code

## Slicing big objects

## Better naming

## Remove duplication

- Exact duplicates
- Non exact duplicates

## nested if statements

- https://wpshout.com/unconditionally-refactoring-nested-statements-cleaner-code/
- the most important characteristic we know to make an if statement under- standable is to make it look like the specification. And this matters more than reducing nesting.

## Making side effects visible

- Aim to reduce side effects
  - use of functional paradigm
- Making it clear what effects a function has on objects helps following along and being less surprised when debugging code.
- use of built in language features to make immutable objects
- you can pass in the objects to be modified as function argument instead of global variable
- bundle the function that makes a side effect on a piece of data with it into a class
- make it clear in a function’s name what side effects it has

## Conditional to polymorphism
- https://www.youtube.com/watch?v=8uJC9wkA204
- https://www.youtube.com/watch?v=SuqrAtXnn1U
- https://stackoverflow.com/questions/48377525/replace-conditional-with-polymorphism

## replace method with method object

- https://www.youtube.com/watch?v=ntjg6rE6lss

## Links

- https://refactoring.guru/refactoring
- https://refactoring.com/catalog/
- https://refactoring.guru/refactoring/catalog
- https://sourcemaking.com/refactoring
- https://dev.to/developerscode/the-dichotomy-of-writing-and-reading-object-oriented-code
- https://www.javacodegeeks.com/2018/04/nine-steps-of-learning-by-refactoring.html
- https://dzone.com/articles/what-is-refactoring
- http://www.lagerweij.com/2011/05/28/code-cleaning-a-refactoring-example-in-50-easy-steps/
- Gilded rose https://www.youtube.com/watch?v=4DTRY1u7cXg
- Example of how to refactor https://www.youtube.com/watch?v=jwJnd9ycs6Q

## Book

- http://amzn.eu/gxL9VgF
-
