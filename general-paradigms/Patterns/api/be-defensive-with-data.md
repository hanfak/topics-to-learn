# Be defensive with your data

- Make sure you deal with immutable return types
  - Make sure that the return type is not a mutable list, or the elements are mutable, thus preventing user from changing it
- use unmodifiable list, or copies
