# 3. Liskov Substitution Principle

- calling code should be able to use an instance of a base class or an instance of a derived class without knowing it, or having to do anything special.
- Example
  - A square is not a rectangle
- if code starts to look like if (shape is Square) ... else if (shape is Rectangle) ..., it can be a “code smell”
- Why?
  - reduce complexity in calling code so that it can work generically on any class or subclass without additional conditional code.
  -

## Links

- https://stackify.com/solid-design-liskov-substitution-principle/
- https://dzone.com/articles/solid-principles-liskov-substitution-principle
