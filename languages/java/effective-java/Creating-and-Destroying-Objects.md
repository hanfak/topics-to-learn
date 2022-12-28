# Creating and Destroying Objects

- [Creating and Destroying Objects](#creating-and-destroying-objects)
	- [Consider static factory methods instead of constructors](#consider-static-factory-methods-instead-of-constructors)
	- [Consider a builder when faced with many constructor params](#consider-a-builder-when-faced-with-many-constructor-params)
	- [Enforce the singleton property when a private constructor or enum type](#enforce-the-singleton-property-when-a-private-constructor-or-enum-type)
	- [Enforce non-instantiability with a private constructor](#enforce-non-instantiability-with-a-private-constructor)
	- [Prefer dependency injection to hard-wiring resources](#prefer-dependency-injection-to-hard-wiring-resources)
	- [Avoid creating unnecessary objects](#avoid-creating-unnecessary-objects)
	- [Eliminate obsolete object references](#eliminate-obsolete-object-references)
	- [Avoid finalizers and cleaners](#avoid-finalizers-and-cleaners)
	- [Prefer try-with-resources to try-finally](#prefer-try-with-resources-to-try-finally)

## Consider static factory methods instead of constructors

-  flexible way of object instantiation


### Pro
- static factories have names, unlike constructors
-  not required to create a new object on each invocation
  - called instance controlled
  - enable singleton and non-instantiability  guarantees
  - allows immutable value class to guarantee no two instances exist
  - forms the basis of Flyweight Pattern
  - Enum types provide this guarantee
-  can return an object of any subtype of their return type
- lends itself to interface-based frameworks
- allow the class of the returned object to vary from call to call as function of input params
- do not require the class of returned object to exist when the class containing the method is written
  - form the basis of service provider frameworks ie jdbc


### Cons
-  classes without public/protected constructors cannot be subclassed
  - encourages composition (which is good)
- hard to find in documentation
- they scale poorly with the increase of (optional) params

### Naming

- from()
- of()
- valueOf()
- instance() or getInstance()
- getType()
- newType()
- type()

## Consider a builder when faced with many constructor params

- Handle increase in params, esp optional ones
  - Solutions:
    - telescoping constructor - scales poorly
    - JavaBeans pattern - need setters
      - causes inconsistency
      - no immutablitiy
- Builder solves these

### Pro
-  static member class
- client code is easy to write
  - fluent style
- incorporate validity checks
  - can throw IllegalStateException
- Can construct any subclass
  - generic builder with recursive type parameters
  - abstract self() simulates self-type which, combined with covariant return typing, obviates need for casting
- flexible

### cons
- cost of creating a builder
- verbose

##  Enforce the singleton property when a private constructor or enum type

### how
- with public final field
- with static factory
- with a single-element enum (preferred)
  - well-defended against reflection
  - prevents serialization issues

### con

- making a class a singleton can make it difficult to test

## Enforce non-instantiability with a private constructor

- class that is simply a grouping of static methods and static fields
- uses
  - group related methods on primitive values or arrays
  - group static methods, including factories
    - default methods are also available (providing we own the interface)
  - group methods on a final class, since we can’t put them in a subclass

### How

- make such classes non-instantiable
  - provide an explanatory comment
  - throw an AssertionError from constructor instead of empty one, to guard against accidental constructions from within the class
  - as a side-effect, this class is now effectively final
    - the class cannot be subclassed as there are no available constructors
    - it is good to document this a make the class itself final

## Prefer dependency injection to hard-wiring resources

- do not use static utility methods or singletons to handle creations of class’ resources
- favour dependency injection by supplying the required resource parametrically
  - testable
  - flexible (esp. with Factory Method pattern
    - Supplier<T> is perfectly suited for representing factories
    - methods that take this interface should typically constrain the factory’s type parameter with a bounded wildcard type
      - the client should be able to pass in a factory that requires any subtype of a specified type
- Can use frameworks to do this

## Avoid creating unnecessary objects

- avoided by using static factory methods
- some object creations are much more expensive than others
  - it may be advisable to cache such objects
  - ie regex patterns, database connections
- immutable objects can trivially be reused
- Use Adapters aka views
  - adapter is an object delegating to a backing object, providing an alternative interface
  - has not state beyond the backing object thus provides a view of it
  - example: keySet() in Map interface
- autoboxing can often subtly create unnecessary objects
- almost never create own object pools
  - JVM gc will almost always outperform such pools
  - exception to this: very expensive objects
    - example: database connection objects
- counterpoint to this is defencive copying

##  Eliminate obsolete object references

- common sources of leaks
  - a resizing-array stack that doesn’t null out its references on pop()
  - classes that manage their own memory
  - caches
    - can be mitigated with WeakHashMap
    - sophisticated caches might need to use java.lang.ref directly
  - listeners and other callbacks
    - APIs that register callbacks but don’t deregister them explicitly
    - can be mitigated with WeakHashMap  
- anticipate such problems before they occur as they can be very costly to fix

## Avoid finalizers and cleaners

- finalizers and cleaners are used to reclaim non-memory resources
  - example: input/output streams, files, etc.
  - Different to deconstructors
- finalizers are unpredictable, dangerous and generally unnecessary
- cleaners are less dangerous than finalizers but still slow, unpredicatble and generally unnecessary

## Cons

- spec makes no guarantee when they’ll be executed
  - their execution is a function of GC algorithm, thus JVM implementation
  - never do anything time-critical in a finalizer or cleaner
  - providing a finalizer may arbitrarily delay reclamation of class’ instances
  - cleaners are a bit better but still run under the control of GC so still the same applies
  - any existing methods that claim to trigger finalization are decade-old traps
    - examples: System.runFinalizerOnExit or Runtim.runFinalizerOnExit
- uncaught exception thrown during finalization is ignored until finalization of that object terminates
  - object is potentially left in corrupted state
  - normally, uncaught exception terminates the executing thread and dumps stacktrace but not if it occurs in finalizer
  - cleaners do not suffer from this problem
- there is a severe performance GC penalty for using finalizers and cleaners
  - finalizers: ~50x slower reclamation
  - cleaners: ~5x slower reclamation, equal to finalizers if they’re used to clean all instance of the class
- finalizers open up classes to finalizer attacks
  - if an exception is thrown during finalization, the finalizer leaves the class unreclaimed
  - attackers can exploit this and run code that shouldnt’ve existed
  - to protect non-final classes against it - write a final finalize() that does nothing
### when
- except as a safety net or to terminate non-critical native resources
### Alternatives

- instead of using finalizers or cleaners simply use AutoCloseable
  - require clients to invoke close() whenever instance is not required
-
## Prefer try-with-resources to try-finally
- Java libraries include many resources that must be closed manually by invoking close()
- closing objects is often overlooked by clients
- try-finally was the best way to guarantee a resource would be closed properly, even when facing exception or return
  - while it doesn’t look bad for a single resource, it doesn’t scale well with the increase of resources required to be closed
  - nested finally block complicate debugging
- try-with-resources suffers none of this issues
  - shorter, more readable than try-finally
  - provides far better diagnostics
  - no exceptions are suppressed
