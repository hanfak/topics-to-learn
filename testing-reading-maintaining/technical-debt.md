# Technical Debt


- [Technical Debt](#technical-debt)
	- [What](#what)
	- [Causes of technical debt](#causes-of-technical-debt)
	- [Examples of technical debt](#examples-of-technical-debt)
	- [Handling technical debt](#handling-technical-debt)
	- [Issues with technical debt](#issues-with-technical-debt)

## What

- that when it is accrued, interest must be paid on it over time. The cost of paying this interest reduces the amount of resources available that could otherwise be spent adding new features and business value.
- when there is too much Technical Debt and all effort is being spent on paying the interest, a system may have to be rewritten before new features can start to be added again.
- Slows down the ability to change software
- All software has technical debt
- technical debt accrues, if so is it done on purpose and accepted that we will have to handle the consequences
- what can happen when developers do not factor their learning back in to their code as they're building it

## Links

- https://dzone.com/articles/what-technical-debt-it-and-how-to-calculate-it

## Causes of technical debt

- Biggest cause of technical debt is delivery schedule pressure, and devs get sloppy and cut corners
- Unmanaged, incorrect, or chaotically changing requirements
- Junior, inexperienced, or unmotivated programmers
- Parallel development streams followed by big-bang merges
- Delayed refactoring or no refactoring
- Poor communication and collaboration
- Poor or inexperienced management
- Bad Development Practices
- Outdated Technology

## Examples of technical debt

- Tight coupling between internal and external dependencies
- Poor test coverage
- Poor quality tests
- Inconsistent code formatting styles
- Hardcoded values (“magic strings”)
- Complex or bloated methods, functions, classes, etc.
- Code duplication
- Redundant or unused code
- Out of date or unsupported third party libraries
- Poor code commenting
- Shared global variables, statics, etc.
- Lack of the Documentation
- Lack of Modularity
- Product bugs

## Forms of tech debt

- Planned Technical Debt
	- when the organization makes an informed decision to generate some technical debt with the full understanding of the consequences (risks and costs).
	- it is critical to be as precise as possible in terms of defining the compromises the organization intends to make.
	- these decisions can accumulate quickly over time, it is imperative to maintain a record of them
- Unintentional Technical Debt
	- arises due to poor practices.
- Unavoidable Technical Debt
	- due to changes in the business and the progress of technology over time that present better solutions.
	- when scope changes are requested mid-project, that result in an immediate cost such as adding a new feature to an existing design to better support mobile delivery.
	- technical debt is created when new business requirements make old code obsolete.

## Handling technical debt

- Technical debt chart on codewall
  - axes: pain and effor to fix
  - items of tech debt placed on axes
  - promote conversations
- Have a story, places todos in code base with description of tech debt and story number
- Need to be mindful, know that debt is accruing and accepting the trade offs for doing it.

## Issues with technical debt

- slows down changes in software
- developer happiness goes down, dont want to work with crap code
- Retain and recruit developers if debt is not addressed

## Links

- https://www.bmc.com/blogs/technical-debt-explained-the-complete-guide-to-understanding-and-dealing-with-technical-debt/
