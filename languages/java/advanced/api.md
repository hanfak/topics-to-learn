# API

- Creating apis is probably the main thing that java is used for
  - Web api
  - library api
- An API is what developers use to achieve some task
  - is useful as used by other software, and resusable
- it establishes a contract between them and the designers of the software, exposing its services through that API.

## Characteristics of good api

- should be easily understandable and discoverable
  - It should be possible to start using it and, ideally, learn how it works without reading its documentation
  - Having example tests is a good replacement for documentation
- it’s important to use consistent naming and conventions.
- Keeping your API minimal is another way to make it easy to use.
- using factory methods instead of constructors is another valuable practice since it allows greater flexibility:
  - you can also return an instance of a subclass or even a null when the method is called with illegal arguments.
- principle of least astonishment should be observed
  - It should do what is expected
  - Example, Optional.of(T t) breaks this as throws nullpointer when t is null, thus needs Optional.ofNullable(T t). When only one method would be needed
-  break apart large interfaces into smaller pieces;
- consider implementing a fluent API,
- never return null
  - emptylist or optional instead
- limit usage of exceptions, and possibly avoid checked ones
-  Regarding method arguments:
  -  avoid long lists of them, especially of the same type;
  -  use the weakest possible type;
  -  keep them in consistent order among different overloads;
  -  consider varargs
