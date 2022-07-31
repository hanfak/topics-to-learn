# 3. Liskov Substitution Principle

- calling code should be able to use an instance of a base class or an instance of a derived class without knowing it, or having to do anything special.
- Example
  - A square is not a rectangle
- As long as an interface doesn't change, the clients don't care if you change the implementation
- if code starts to look like if (shape is Square) ... else if (shape is Rectangle) ..., it can be a “code smell”
- Why?
  - reduce complexity in calling code so that it can work generically on any class or subclass without additional conditional code.
  -


## Testing

- https://blog.caplin.com/2010/09/30/a-junit-trick-for-ensuring-solid-design/

## Issues

- Sometimes you do want to have different behaviour to the super class
- It was original stated by
- Even the author says, the idea of substitutability was informal and was not evening in formal definition (https://dl.acm.org/doi/10.1145/197320.197383, https://www.youtube.com/watch?v=-Z-17h3jG0A)


## Links

- https://stackify.com/solid-design-liskov-substitution-principle/
- https://dzone.com/articles/solid-principles-liskov-substitution-principle
- https://medium.com/hackernoon/the-liskov-substitution-principle-and-why-you-might-want-to-enforce-it-6f5bbb05c06d
- https://reflectoring.io/lsp-explained/
