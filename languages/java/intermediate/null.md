# Null

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Null](#null)
	- [what it means](#what-it-means)
	- [Alternative](#alternative)
		- [How to handle](#how-to-handle)
	- [Code smell](#code-smell)

<!-- /TOC -->

- https://stackoverflow.com/questions/2707322/what-is-null-in-java

## what it means

- Value was never initialized (whether accidentally or on purpose)
- Value is not valid
- Value is not needed
- No such value exists
- Something went terribly wrong and something that should be there is not

## Alternative

- Use Optional.empty()
  - Example, ask the database for a Customer with a given ID. Previously, you might have used null to represent this, but that could be ambiguous – does it mean the customer wasn’t found? Or that there’s a customer with that ID, but has no values? Or was null returned because the connection to the database failed? By returning an empty Optional, you’ve removed the ambiguity – there’s no customer with that ID.
  - Not a solution to everywhere you find a null.  But if a method is deliberately returning a null value to mean “not found” or “I don’t have one of those”, this is a good candidate for returning an Optional.
- use of final fields, so objects are alwasy initialized in constructors
- Use of builders and factories to validate correct combinations before instantiation
- not using nulls in the core of your application (i.e. pushing all checks to the edges)
- @NotNull/@Nullable.
  - One of the problems with complex code bases is understanding what are actually valid values. If you’re checking for null parameters, try putting @NotNull on the signature and seeing if null values are ever passed.  If nulls are never passed, you can remove the null check.

### How to handle

- KISS
  ```java
  if (Optional.ofNullable(myVariable).isPresent()) // bad
  if (Objects.nonNull(myVariable)) // better, but still bad
  if (myVariable != null) // good
  ```
- Use Objects Methods as Stream Predicates
  ```java
  myStream.filter(Objects::nonNull)
  myStream.anyMatch(Objects::isNull)
  ```
- Never Pass Null as an Argument
  - Passing null to indicate that there’s no value for a given argument might seem like a viable option. Because:
    - You need to read the function’s implementation and figure out if it, and potentially every affected function down the way, can handle null value correctly.
    - You have to always be careful when changing function’s implementation not to throw away something that might handle nulls for its users. Otherwise, you have to search through the whole source code to check if null is being passed anywhere.
  -  make sure things are safe from the outside
    - you can give up on the rule when dealing with private methods
	- If you need a T, ask for it; if you can get by without one, then don’t ask for it. For an operation that can have an optional parameter, create two methods: one with the parameter and one without
- Validate Public API Arguments
  - when you’re exposing a public API, you have no control over its users and what they pass to your functions.
  - always check the arguments being passed to your public APIs for correctness
  - consider using the requireNonNull function from the Objects class:
    ```java
    public Foo(Bar bar, Baz baz) {
        this.bar = Objects.requireNonNull(bar, "bar must not be null");
        this.baz = Objects.requireNonNull(baz, "baz must not be null");
    }
    ```
- Use Optional
  - designed specifically to indicate that a return value might be missing
  - calling a method with Optional as the return value has to explicitly handle the case when the value is not present.
- Return Empty Collections or optionals Instead of Null
  - we should avoid returning null or complicating things with Optional and return an empty collection when there are no values to fill it with.
- Optional Ain’t for Fields
  - By means of encapsulation, you should have full control over the field's value, including null.
  - making fields explicitly Optional might bring you weird problems like:
    - How should you write a constructor or setter for such a field?
    - You have to deal with the Optional even in cases when you’re sure that the value is there.
    - How should automappers handle those fields?
- Use Exceptions Over Nulls
  - when you might see people using null is exceptional situations.
  - This is an inherently error prone practice, as critical errors can be omitted or resurface in different places of the system, causing debugging to be a pain.
  - Therefore, always throw an exception instead of returning null if something went wrong.
- Avoid Initializing Variables to Null
	- Initializing a variable to null might leak null unintentionally if you are not careful with your error-handling code.
	- For complex initialization, move all the initialization logic to a method.
	- instead of this
		```java
		public String getEllipsifiedPageSummary(Path path) {
			String summary = null;
			Resource resource = this.resolver.resolve(path);
			if (resource.exists()) {
				ValueMap properties = resource.getProperties();
				summary = properties.get("summary");
			} else {
				summary = "";
			}
			return ellipsify(summary);
		}
		```
	- do this
		```java
		public String getEllipsifiedPageSummary(Path path) {
			var summary = getPageSummary(path);
			return ellipsify(summary);
		}
		public String getPageSummary(Path path) {
			var resource = this.resolver.resolve(path);
			if (!resource.exists()) {
				return "";
			}
			var properties = resource.getProperties();
			return properties.get("summary");
		}
		```
- Test Your Code
- https://dzone.com/articles/10-tips-to-handle-null-effectively

## Code smell

- Leads to lots of null checks
  - If application is well designed, and we are incharge  of what gets passed to an object, we can avoid null checks as we know that null will never get passed to an object (constructor or method)
- nulls could mean lots of things
- Exception handling. Returning null for an Exceptional case is very unfriendly, and unexpected from the caller’s point of view.  It can lead to NullPointerException further down the line, or at least more of the pervasive null checks (without a clear idea of why the value is null).  Throwing a descriptive Exception is much more valuable for those downstream.
