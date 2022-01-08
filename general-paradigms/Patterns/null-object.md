# Null Object Pattern

## What

- Special case of strategy pattern
- A null object refers to an object without any reference or an object defined with neutral/null functionality/behavior.
  - These null objects need to be checked to ensure that they are not null while accessing any member or invoking any methods.
  - Otherwise, throw nullpointer exception
- The intent of a Null Object is to encapsulate the absence of an object by providing a substitutable alternative that offers suitable default do nothing behavior.
- the class wishes to treat a collaborator that does nothing the same way it treats one that actually provides behavior.
- In most object-oriented programming languages, we're not allowed to use a null reference.
  - In java we are, that's why we're often forced to write null check
  - Use a guard statement to check if null
  - If too many guard statements not good
- The intent of the Null Object Pattern is to minimize that kind of null check.
  - we can identify the null behavior and encapsulate it in the type expected by the client code
- As null objects should not have any state, there's no need to create identical instances multiple times.
  - Thus, we'll often implement null objects as singletons.

## How

- Instead of checking for the null object, we define null behavior or call do-nothing behavior.
- These null objects can also be used to provide default behavior in case data is unavailable.
- Parts
  - Client requires an instance of AbstractObject
  - AbstractObject defines the contract Client expects – it may also contain shared logic for the implementing classes
  - RealObject implements AbstractObject and provides real behavior
  - NullObject implements AbstractObject and provides neutral behavior
- Can now use Java 8 Optional


## Advantages

- The null object pattern can also be used to act as a stub for testing, in case a resource is unavailable for testing.
- that a null object is very predictable and has no side effects — it does nothing.
- It defines class hierarchies consisting of real objects and null objects. Null objects can be used in place of real objects when the object is expected to do nothing. Whenever client code expects a real object, it can also take a null object.
- makes the client code simple. Clients can treat real collaborators and null collaborators uniformly. Clients normally don’t know whether they’re dealing with a real or a null collaborator. This simplifies client code, because it avoids having to write testing code which handles the null collaborator specially.

## Drawbacks

- Can be difficult to implement if various clients do not agree on how the null object should do nothing as when your AbstractObject interface is not well defined.
- Can necessitate creating a new NullObject class for every new AbstractObject class.
- The price of getting rid of conditionals is creating yet another new class.
