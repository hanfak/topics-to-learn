# Methods Common to All Objects

- [Methods Common to All Objects](#methods-common-to-all-objects)
	- [Obey the general contract when overriding equals()](#obey-the-general-contract-when-overriding-equals)
	- [Always override hashCode() when overriding equals()](#always-override-hashcode-when-overriding-equals)
	- [Always override toString()](#always-override-tostring)
	- [Override clone() judiciously](#override-clone-judiciously)
	- [Consider implementing Comparable](#consider-implementing-comparable)


## Obey the general contract when overriding equals()

- The == operator tests for instance equality;
- whereas the equals() method may be overriden to test for value equality.
  - But by default it is the same as ==
- When to use default impl of equals()
  - Each instance of the class is inherently unique.
  - There is no need for the class to provide a “logical equality” test.
    - no need for two equivalent regexes to compare equal if this functionality is not needed by client code
  - A superclass has already overridden equals, and the superclass behavior is appropriate for this class.
  - The class is private or package-private, and you are certain that its equals() method will never be invoked.
- There is usually no need to explicitly test for null in the equals() method
  - because the standard implementation requires an instanceof() check, which is specified to return false if null is provided.
### Contract
- violation of this contract means it is uncertain how other objects will behave when confronted with our object
- (reflexivity) x.equals(x) == true, for x != null
  - hard to violate unintentionally
- It is generally hard to fulfil the requirement of symmetry when creating a subclass with an equals() method that is interoperable with the super class.
  - subclass.equals(superclass) and superclass.equals(subclass) must be equal, but you may not always be able to change the implementation of the equals() method in the super class
- transitivity requires that: if a.equals(b) and b.equals(c), then a.equals(c) must be true.
  - no way to extend an instantiable class and add a value component while preserving the equals contract.
  - This is because for class_with_added_value.equals(superclass) to be symmetrical to superclass.equals(class_with_added_value), the equals() method in the subclass must ignore the additional value component when the superclass passed as the argument. However, when comparing one instance of the subclass with another instance of the subclass, the equals() method will also compare the additional value component. As a result, when class_with_added_value_1.equals(superclass) and class_with_added_value_2.equals(superclass) are true, class_with_added_value_1.equals(class_with_added_value_2) may not be true.
- (consistency) x.equals(y) == x.equals(y), for x, y != null
  -  Do not write an equals() method that depends on unreliable resources
    - e.g., IP addresses as opposed to URLs, because DNS look-up may fail
- (non-nullity) x.equals(null) == false, for x != null
  - hard to violate unintentionally, unless an exception is thrown instead of returning false
### How to implement

- The general steps to implement an equals() method is as follows:
  - Use the == operator to check if the argument is a reference to this object.
  - Use the instanceof operator to check if the argument has the correct type.
  - Cast the argument to the correct type.
  - For each "significant" field in the class, check if that field of the argument matches the corresponding field of this object.
  - When you are finished writing your equals method, ask yourself three questions: Is it symmetric? Is it transitive? Is it consistent?
  - When an object has a canonical form, and the equality comparisons of fields are complex, consider storing a canonical form of the object to be used in the equals() method.
    - Note that this canonical form would have to be updated if the object is mutable.
  - Performance of the equals() method depends on the order of the fields being compared. If possible, try to compare fields that are most likely to be different first.
  - Use automatic generation of equals() and hashcode() methods provided by @AutoValue annotation.
#### Comparing types
- For primitive fields whose type is not float or double, use the == operator for comparisons
- for object reference fields, call the equals() method recursively
- for float fields, use the static Float.compare(float, float) method
- for double fields, use Double.compare(double, double).
- For array fields, apply these guidelines to each element.
  - If every element in an array field is significant, use one of the Arrays.equals() methods.
- Some object reference fields may legitimately contain null.
  - To avoid NullPointerException, check such fields for equality using the static method Objects.equals(Object, Object).
## Always override hashCode() when overriding equals()
- violating this prevents proper functioning of hash-based collections (ie hashset, hashmaps)
- Consider lazy initialization if calculation of hashcode is resource intensive and not always required.
- worst possible hash-code implementation is returning the same number
  - degrades performance horrifically
- rely on the Object.hashCode(...) to compute the hash-code unless performance is very important

### Contract

- (consistency) x.hashCode() == x.hashCode(), for x != null
- (equality) x.equals(y) => (x.hashCode() == y.hashCode()), for x, y != null
- if a.equals(b) is false then a.hashCode() doesn't have to be different of b.hashCode()

## Always override toString()

-  unless a superclass already did it
- Provide information of all relevant members of the object in the toString() output.
  -  It needs to be a full representation of the object and every information contained in the toString representation should be accessible in some other way in order to avoid programmers to parse the String representation.
- makes systems using the class easier to debug
  - disadvantage: once specified, it’s for-life, users will rely on it
- don’t override toString() on
  - static utility class
  - enum types
- rely on IDE to create a good toString() implementation
## Override clone() judiciously

- Avoid implementing Cloneable if possible as it a fragile language feature, requiring many extralinguistic factors. It requires the class and all of its superclasses obey a complex, unenforceable, thinly documented protocol.
- A better approach to object copying is to provide a copy constructor or copy factory.
-
### impl

- All classes that implement Cloneable should override clone with a public method whose return type is the class itself. This method should first call super.clone, then fix any fields that need fixing. Typically, this means copying any mutable objects that comprise the internal "deep structure" of the object and replacing the clone's references to these objects with references to their copies.
- The only exception is arrays which should generally be copied using the clone() method. Note: clone() still doesn't copy arrays of 2 or more dimensions deeply.
## Consider implementing Comparable

- implementing Comparable, class indicates its instances follow natural ordering
  - This is fixed for those objects
  - whenever a value class has sensible ordering, Comparable should be implemented
- By implementing Comparable interface, you allow the class to interoperate with all of the generic algorithms and collections that depend on this interface. ie treeset
-  there is no way to extend an instantiable class with a new value component while preserving the compareTo() contract, unless you are willing to forgo the benefits of object-oriented abstraction.
  -  to preserve the compareTo() contract in a subclass, the compareTo() must be implemented in a way such that objects can only ever be compared to other objects of the exact same class, hence violating Liskov substitution principle.
-  results returned by equals() and compareTo() should generally be consistent;
- If a class has multiple significant fields, the order in which you compare them is critical.
  - Start with the most significant field and work your way down.
- Do not use comparison that rely on the fact that the difference between two values is negative if the first value is less than the second, zero if the two values are equal, and positive if the first value is greater:
  - e.g., return instance_a.value - instance_b.value.
  - This approach suffers from the dangers relating to integer overflows and artifacts from floating point arithmetic.
  - Use the static compare method instead: e.g., Integer.compare(instance_a.value, instance_b.value).
- static compare() methods to primitive, as have been added to all boxed primitive classes, instead of < and >
- do not use hashCode arithmetics-based comparisons
  - though somewhat more performant, they are fraught with danger from integer overflow and FP arithmetic artifacts

### Contract
- (reflexivity) (x.compareTo(y) == 0) => (sgn(x.compareTo(z) == sgn(y.compareTo(z)), for x, y, z != null
- (symmetry) sgn(x.compareTo(y)) == -sgn(y.compareTo(x)), for x, y != null
  - helps imposing total order
-  (transitivity) (x.compareTo(y) && y.compareTo(z)) > 0 => (x.compareTo(z)) > 0, for x, y, z != null
  - helps imposing total order
- (optional consistency with equals) (x.compareTo(y) == 0) <=> (x.equals(y)), for x, y != null
  - if violated, still will yield valid comparisons but will generally not guarantee obeying the general contract for collections and maps
  - examples: java.util.BigDecimal in HashSet and TreeSet
  - BigDecimal("1.0") and BigDecimal("1.00") compares unequal when using the equals() method but compares equal when using the compareTo() method. As a result, after inserting both into a TreeSet, there will only be one element. Whereas after inserting both into a Hashset, there will be two elements. This is because TreeSet and HashSet uses compareTo() and equals() respectively for comparison.
