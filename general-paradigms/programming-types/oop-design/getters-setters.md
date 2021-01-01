# Getters and Setters

- Using a getter to return an imutable type (ie list or custom type), should return a clone of the object, to keep object immutable
  - Also be aware object graph having mutable types
- The idea is that getters encapsulate how values are represented in an object, providing a consistent approach across a codebase. 
- It also allows for protection against aliasing, for example, by cloning collections before returning them

## Reasons against

- https://www.yegor256.com/2014/09/16/getters-and-setters-are-evil.html
- https://codurance.com/2018/03/20/getters-and-setters-considered-harmful/
- Make fields public final, so they cannot be changed (ie immutable)
- dont ask for field from its object, ask objec to do the work (delegate it) and then call it
- http://www.yegor256.com/2014/09/16/getters-and-setters-are-evil.html
- https://dzone.com/articles/getters-and-setters-considered-harmful
