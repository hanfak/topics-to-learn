# Decorator Pattern

- The Decorator pattern allows the addition of behaviour to existing classes without changing the original class
- The pattern also allows the “wrapping” of multiple decorators inside each other to compose behaviours.
  - Thus delegating behaviour to the wrapped object
- Implements open/closed principle
- The decorator pattern typically starts with an abstraction of some behaviour.
- A decorator implements the same interface as the class it is decorating. It also contains a reference to the decorated (“wrapped”) instance.
- The decorator delegates to the “wrapped” instance of a decorator
- The key thing here is that extra runtime behaviour has been added without having to modify the original class
- keep software soft because existing behaviour can be extended and composed without having to change existing implementation code
- Decorator works best when you have just a single I/O channel...[it] is a great way to allow to dynamically compose the way we apply processing to it.


## Link

- https://www.yegor256.com/2015/02/26/composable-decorators.html
