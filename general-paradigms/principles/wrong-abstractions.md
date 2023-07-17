# Wrong abstractions

- What happens when refactoring or DRYing code is done too early
  - Which can lead to redoing these abstractions 
- duplication is far cheaper than the wrong abstraction
- The premature abstraction leaves an imprint for how code should be done in future, so future changes will try and maintain the abstraction which leads to worse code & complexity instead of creating a better abstraction
  - Sunk cost fallacy

## Counter 

- Wait for duplication to be repeated 3 times before abstracting 
- Duplication is ok, up to a point
- When dealing with wrong abstraction
  - inline and start again, maybe extract out new abstraction if necessary

## Signs 

-  If you find yourself passing parameters and adding conditional paths through shared code, the abstraction is incorrect.

## Links 

- https://sandimetz.com/blog/2016/1/20/the-wrong-abstraction
- https://alexkondov.com/the-cost-of-wrong-abstractions/
- https://www.codewithjason.com/duplication-cheaper-wrong-abstraction/
  - an opposite view
- https://blog.awesomesoftwareengineer.com/p/duplication-is-better-than-wrong-abstraction