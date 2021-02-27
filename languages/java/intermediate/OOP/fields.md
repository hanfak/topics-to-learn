# Fields/state

- A field is a data member of a class. Unless specified otherwise, a field can be public, static, not static and final

## static final
## final
## static variables

## Variable scope

## When to use fields

- If it will be used by the whole class not just a method
  - This depends if the class is a single method class (command pattern)
- It is the state of the instance
- There is only one instance of the object passed into the field which is fixed at compile time
  - If using dependency injection, this implementation can be different at runtime
- You should never use a field to simplify passing data from one method to another method.
- The object of the field will always be used in same way ie call to some instance method to apply some logic
  - Where as the parameter, depending on its state may be used differently


### When to use over a method variable or parameters

- Parameters constantly change, when the method is called.

## Links
