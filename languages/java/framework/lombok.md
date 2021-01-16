# Lombok

- https://projectlombok.org/

## Why?

- Reduce verbosity of writing common java boiler plate code
- To increase coding productivity, by reducing amount of time to write boilerplate code
- Well maintained library

## Costs

- Bugs appear often
- static imports on builders, with poor compile errors
  - compile erros happens in build, and not spotted in IDE
- @builders can leave objects in incorrect state
- Increase build time
- Magic code, makes it hard to debug what the problem is
- Will not play nice with some other libraries
- Delomboking (a plugin) may not give an accurate representation of what lombok is doing, and it is not really nice (does not match code style)
- Does things with the compiler in an non standard way
- It mainly hides implementation details
- upgrading (library or java version) can cause ripple affects in codebase
- Can end up having lots of annotations stacked up on each other, and added parameters. Plus annotations from other libraries/frameworks, end up being verbose in other ways
- Removing it can be hard, as it pollutes the whole of the code base
- Hacking java into somethiing that it is not, instead use another language with these features built in
- IT can confuse IDEs, thus need to rely on plugins and upgrades to IDE
- To get it working  correctly will need to fix maven config gradle scripts, which main not be feasible

## Links

- https://medium.com/@ppbruna/why-you-should-not-use-lombok-f7556662e8c3
- https://medium.com/@vgonzalo/dont-use-lombok-672418daa819
- https://artofcode.wordpress.com/2018/12/18/dont-use-lombok/



NOTE: With any library,
- be sure to understand it's pros and cons (esp around secruity and legal), does it meet cost benefit for usage
- Is it well maintained, number of contributors, passing tests, good test coverage, usages in production code
- Good documentation, good example tests
- test it
- write poc (proof of concept)
- try it out but be able to make it easy to remove if not working out
  - The only way it can be found as useful is in production
- avoid having to build lots of hacks or engineer solutions to bugs or needed features which are not suited to library
- Avoid having to have comments or readme/faqs to help user deal with problem
