# Classes and Interfaces

- [Classes and Interfaces](#classes-and-interfaces)
	- [Minimise the accessibility of classes and members](#minimise-the-accessibility-of-classes-and-members)
	- [Favour accessors over public fields in public classes](#favour-accessors-over-public-fields-in-public-classes)
	- [Minimise mutability](#minimise-mutability)
	- [Favour composition over inheritance](#favour-composition-over-inheritance)
	- [Design and document for inheritance or else prohibit it](#design-and-document-for-inheritance-or-else-prohibit-it)
	- [Prefer interfaces to abstract classes](#prefer-interfaces-to-abstract-classes)
	- [Design interfaces for posterity](#design-interfaces-for-posterity)
	- [Use interfaces only to define types](#use-interfaces-only-to-define-types)
	- [Prefer class hierarchies to tagged classes](#prefer-class-hierarchies-to-tagged-classes)
	- [Favor static member classes over nonstatic](#favor-static-member-classes-over-nonstatic)
	- [Limit source files to a single top-level class](#limit-source-files-to-a-single-top-level-class)

## Minimise the accessibility of classes and members

- enforcing encapsulation
  - Speeds up the system development as components can be developed in parallel
  - Enables effective performance tuning. Components can be optimized separately without affecting the others
    - isolation -> does not influence correctness of others
  - reduces maintenance costs
    - easier reasoning/debugging/replacement
  - Increases software reuse as components aren’t tightly coupled
    - decoupled components usually provide use in contexts beyond original design
  - Decrease the risk in building large systems, improves resilience
    - individual components may prove successful even if the system does not
- Make accessibility as low as possible. Work on a public API that you want to expose and try not to give access to implementation details.
- About accessors for members (fields, methods, nested classes, and nested interfaces)
  - public
    - The member is accessible from anywhere.
  - package-private
    - The member is accessible from any class in the package where it is declared. Technically known as default access, this is the access level you get if no access modifier is specified (except for interface members, which are public by default).
  - protected
    - The member is accessible from subclasses of the class where it is declared (subject to a few restrictions) and from any class in the package where it is declared.
    - A protected member of an exported (i.e., public) class represents a public commitment to an implementation detail. The need for such protected members should be relatively rare.
  - private
    - The member is accessible only from the top-level class where it is declared.
  - Both private and package-private members are part of a class's implementation and do not normally impact its exported API. These fields can, however, "leak" into the exported API if the class implements Serializable.
- top level Classes and Interfaces can only be public or package private
- If a top-level class or interface can be made package-private, it should be.
  - By making it package-private, you make it part of the implementation rather than the exported API, and you can modify it, replace it, or eliminate it in a subsequent release without fear of harming existing clients.
- If a package-private top-level class or interface is used by only one class, consider making the top-level class a private static nested class of the sole class that uses it.
- Instance fields of public classes should rarely be public.
  - If an instance field is nonfinal or is a reference to a mutable object, then by making it public, you give up the ability to:
    - limit the values that can be stored in the field
    - enforce invariants involving the field
    - take any action when the field is modified, so classes with public mutable fields are not generally thread-safe.
-  a nonzero-length array is always mutable, so it is wrong for a class to have a public static final array field, or an accessor that returns such a field.
  - Issues of IDEs generating getters for these fields
  - To get access to an array
  There are generally two ways around it:
    - Make the array private, and let the accessor return an immutable List (e.g., construct one using Collections.unmodifiableList(Arrays.asList(THE_ARRAY)).
    - Make the array private, and let the accessor return a copy of the array using clone().
- Module system
  - Helps with issues with public accessor which you dont want to expose to the consumer
  - A module is a grouping of packages, like a package is a grouping of classes.
  - A module may explicitly export some of its packages via export declarations in its module declaration (which is by convention contained in a source file named module-info.java).
  - Public and protected members of unexported packages in a module are inaccessible outside the module; within the module, accessibility is unaffected by export declarations.
  - Public and protected members of public classes in unexported packages give rise to the two implicit access levels, which are intramodular analogues of the normal public and protected levels. The need for this kind of sharing is relatively rare and can often be eliminated by rearranging the classes within your packages.

## Favour accessors over public fields in public classes

- Public classes should never expose its fields. Doing this will prevent you to change its representation in the future.
- Package private or private nested classes, can, on the contrary, expose their fields since it won't be part of the API.
- Public classes should never expose mutable fields.

## Minimise mutability

- immutable classes are classes whose instances cannot be modified
  - all of the data in the object is fixed for the lifetime of the object
  - EG java.lang.String, the boxed primitive classes, BigInteger and BigDecimal
- Why
  -  easier to design, implement and use than mutable classes
  - are simple
  - has always exactly one state
    - the state in which it was created they are easier to use reliably
  -  are inherently thread-safe (they require no synchronisation)
    - thus can be shared freely, promoting reuse
    - no defensive copies necessary
    - their internals can be shared freely
  - make great building blocks for other objects
    - they also make great map keys or set elements
  - provide atomicity for free
- immutable classes are easier to realise using functional, rather than imperative approach
- How
  - Don't provide methods that modify the object's state
    - no setter methods
  - Ensure that the class can't be extended
    - The simplest way to do this is to declare the class as final.
    - to make the constructor private and construct instances in factory methods
      - make default constructor (no args) private and throw AssertionError
  - Make all fields final
    - Exceptions may be made as long as there are no externally visible change in the object's state.
    - One example is to have a nonfinal field serve as cache for the result of the an expensive computation.
  - Make all fields private
  - Ensure exclusive access to any mutable components
    - If the class has any fields that refer to mutable objects, ensure that clients of the class cannot obtain references to these objects.
    - Never initialize such a field to a client-provided object reference or return the field from an accessor.
    - Make defensive copies in constructors, accessors, and readObject() methods.
  - Constructors should create fully initialized objects with all of their invariants established.
- The major disadvantage of immutable classes is that
  - they require a separate object for each distinct value.
  - Creating these objects can be costly, especially if they are large.
  - Solution
    - One way around this is to provide a package-private / public mutable companion class
    - String has Stringbuilder
-  it was not widely understood that immutable classes had to be effectively final when BigInteger and BigDecimal were written, so all of their methods may be overridden.
  - Unfortunately, this could not be corrected after the fact while preserving backward compatibility.
  - If you write a class whose security depends on the immutability of a BigInteger or BigDecimal argument from an untrusted client, you must check to see that the argument is a "real" BigInteger or BigDecimal , rather than an instance of an untrusted subclass.    
- If you choose to have your immutable class implement Serializable and it contains one or more fields that refer to mutable objects
  - you must provide an explicit readObject or readResolve method
  - use the ObjectOutputStream.writeUnshared and ObjectInputStream.readUnshared methods, even if the default serialized form is acceptable.
  - Otherwise an attacker could create a mutable instance of your class.
- If object is mutable, limit it

## Favour composition over inheritance

- applies to implementation inheritance (extends), not interface inheritance
### what
- inheritance allows classes extends (subclass) a non final class (becomes parent/superclass), thus gain it's behaviour for free
  - If parent class has abstract methods, it must be implemented in the child/subclass class if that class want to be instantiated.
  - abstract methods allow subclasses to implement subclass specific behaviour which is different to the parent class
    - This can also apply to non abstract methods in the parent class, if not overridden by child class, they use the default impl from the parent class
- inheritance is a powerful way to achieve code reuse
- This also allows for polymorphism, as the subclass can be defined by it's parent class type
### bad
- can lead to fragile software if employed inappropriately
-  violates encapsulation
  - subclass depends on implementation details of the superclass - both must evolve in tandem, coupled
    - Can lead to complex hierarchies, hard to refactor
  - related cause of fragility is that their superclass can acquire new methods in subsequent releases
    - subclasses can break
  -  E.g., the parent class may add a public setter to a private field, essentially making the class publicly mutable.
  - When overriding a method, you cannot be sure whether the behavior any of the (non-overriden) methods changed, because the implementation of such other methods might depend on the overriden method.
- Can only extend one class, no multiple inheritance
  - diamond problem, inheriting same method from multiple superclasses, which one to use?
- if extending a class, but dont need all the behaviour
  - throw unsupportedException, but breaks liskov substitution and the polymorphic contract
- Causes user to decide early on what the design is and extract out reuse, but this can change and harder to change design once created with inheritance
### when
- within a package (where sub- and super-class are under control of the same programmers)
- if a class specifically is designed and documented for inheritance
- only appropriate for classes that pass the “is-a” test
  - answer truthfully to question “If B extended A, is B really an A?”
  - This violated a lot in java libraries
### alternative - use Composition
- composition:
  - Create a new class that has as its member an instance/component of the existing class (i.e., the class that would otherwise be extended).
  - This new class will delegate the behaviour it wants to the component
  - component can be instantiated in the field or inside a method, but better to inject (method arg or constructor)
- forwarding aka decorator:
  - Instead of having the new class hold a direct reference to the existing class, have it hold a reference to a forward class – another class that has the same public API as the existing class, and wraps the existing class by simply forwarding each call to the actual method on the instance of the existing class.
  - This also prevents the additional of new methods on the existing class from having any impact on the new class.
  - This idea is used in multiple patterns
#### Benefits
- they don’t depend on the implementation details of the existing class
- issues with inheritance are removed
- you can define your own API for your class
#### bad
- disadvantages of wrapper classes are few:
  - not suited for use in callback frameworks (callbacks elude the wrapper - SELF problem)
  - theoretical performance and memory impacts
  - tedious to write forwarding classes

## Design and document for inheritance or else prohibit it

- Document precisely the effects of overriding any method.
  - document any self-use of overridable methods.
  - The description is to be put in a special section of the specification, labeled "Implementation Requirements," which is generated by the Javadoc tag @implSpec. The documentation should be in the method calling the overridable method, explaining how the overridable method is used.
- To allow programmers to write efficient subclasses without undue pain, a class may have to provide hooks into its internal workings in the form of judiciously chosen protected methods.
- The only way to test a class designed for inheritance is to write subclasses.
- Constructors must not invoke overridable methods, directly or indirectly.
  - Because constructor of superclass are called before the constructor of the subclass is done initializing the entire class, if the constructor of the superclass calls an overriden method that depends on certain state of the class having been set up by the constructor of the subclass, the class may not behave as expected.
- If you do decide to implement either Cloneable or Serializable in a class that is designed for inheritance, you should be aware that because the clone() and readObject() methods behave a lot like constructors, a similar restriction applies: neither clone() nor readObject() may invoke an overridable method, directly or indirectly.
  - In the case of readObject(), the overriding method will run before the subclass's state has been deserialized.
  - In the case of clone(), the overriding method will run before the subclass's clone() method has a chance to fix the clone's state.
  - If you decide to implement Serializable in a class designed for inheritance and the class has a readResolve() or writeReplace() method, you must make the readResolve() or writeReplace() method protected rather than private. If these methods are private, they will be silently ignored by subclasses.
- To enable safer subclassing, it is possible to eliminate a class's self-use of overridable methods mechanically
  - Move the body of each overridable method to a private "helper method" and have each overridable method invoke its private helper method. Then replace each self-use of an overridable method with a direct invocation of the overridable method's private helper method.
- best approach is to prohibit subclassing in classes that are not designed and documented for safe subclassing
  - prohibit inheritance on classes implementing an interface that captures its essence
  - for other classes, ensure at least that the class never invokes any of its overridable methods and document this

## Prefer interfaces to abstract classes

- Java permits only single inherinance.
- Interfaces are ideal for designing mixins.
  - A mixin can be thought of as a type that a class can implement in addition to its "primary type", to declare that it provides some optional behavior
- Intefaces allow for the construction of nonhierarchical type frameworks.
- Interfaces enable safe, powerful functionality enhancements via the wrapper class idiom.
  - A wrapper class is one that
    - (a) holds a reference to the base class to be extended
    - (b) implements the interface of the base class
    - (c) forwards any methods on the interface to the methods on the base class held as reference.
  - If abstract classes were used instead, the programmer who wants to add functionality has no choice but to use inheritance instead, which is more fragile.
- When there is an obvious implementation of an interface method in terms of other interface methods, consider providing implementation assistance to programmers in the form of a default method.
-  skeletal implementation classes are called Abstract Interface, where Interface is the name of the interface they implement
### downsides
- Interfaces are limited in certain aspects: e.g., inability to provide default implementations for hashCode() or equals() method, and inability to contain instances field or nonpublic static members.
### writing an implementation class
- study the interface and decide which methods are the primitives in terms of which the others can be implemented. These primitives will be the abstract methods in your skeletal implementation.
- provide default methods in the interface for all of the methods that can be implemented directly atop the primitives
- If the primitives and default methods cover the interface, you're done, and have no need for a skeletal implementation class.
- write a class declared to implement the interface, with implementations of all of the remaining interface methods. The class may contain any non public fields ands methods appropriate to the task.

## Design interfaces for posterity
## Use interfaces only to define types
## Prefer class hierarchies to tagged classes
## Favour static member classes over non static
## Limit source files to a single top-level class
