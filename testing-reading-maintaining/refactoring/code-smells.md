# Code Smells

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Code Smells](#code-smells)
	- [Types](#types)
		- [Code Smells Within Classes](#code-smells-within-classes)
			- [Comments](#comments)
			- [Long Method](#long-method)
			- [Long Parameter List](#long-parameter-list)
			- [Duplicated code](#duplicated-code)
			- [Conditional Complexity](#conditional-complexity)
			- [Combinatorial Explosion](#combinatorial-explosion)
			- [Large Class](#large-class)
			- [Mysterious Name](#mysterious-name)
			- [Type Embedded in Name](#type-embedded-in-name)
			- [Uncommunicative Name](#uncommunicative-name)
			- [Inconsistent Names](#inconsistent-names)
			- [Dead Code](#dead-code)
			- [Speculative Generality](#speculative-generality)
			- [Oddball Solution](#oddball-solution)
			- [Temporary Field](#temporary-field)
			- [Switch Statements](#switch-statements)
			- [Loops](#loops)
		- [Code Smells Between Classes](#code-smells-between-classes)
			- [Alternative Classes with Different Interfaces](#alternative-classes-with-different-interfaces)
			- [Primitive Obsession](#primitive-obsession)
			- [Data Class](#data-class)
			- [Data Clumps](#data-clumps)
			- [Refused Bequest](#refused-bequest)
			- [Inappropriate Intimacy](#inappropriate-intimacy)
			- [Indecent Exposure](#indecent-exposure)
			- [Feature Envy](#feature-envy)
			- [Lazy Class](#lazy-class)
			- [Middle Man](#middle-man)
			- [Message Chains](#message-chains)
			- [Divergent Change](#divergent-change)
			- [Shotgun Surgery](#shotgun-surgery)
			- [Parallel Inheritance Hierarchies](#parallel-inheritance-hierarchies)
			- [Incomplete Library Class](#incomplete-library-class)
			- [Solution Sprawl](#solution-sprawl)
			- [Global Data](#global-data)
			- [Mutable Data](#mutable-data)
	- [Bad Code Smells Taxonmy](#bad-code-smells-taxonmy)
		- [The Bloaters](#the-bloaters)
		- [The Object-Orientation Abusers](#the-object-orientation-abusers)
		- [The Change Preventers](#the-change-preventers)
		- [The Dispensables](#the-dispensables)
		- [The Couplers](#the-couplers)
	- [Links](#links)

<!-- /TOC -->

- A code smell is a surface indication that usually corresponds to a deeper problem in the system.
- These are issues which may or may not cause problems later, this is a trade off
- It helps you think, you may want this as it is better for your design
- You have to understand your code, your project and the system you're supporting, to make a decision on whether something is smell (and should be refactored) or not
	- There no metric to say that code smell means refactor
- There can lots of different code smells, and they can be defined per codebase, per team, per department, per language, per architecture etc
	- These conventions/opinions can have higher or lower weight depending on senior/team leads
	- To maintian should use static analysis tools or fitness tests to check what conventions you want to maintain

## Types

### Code Smells Within Classes

#### Comments

- A method is filled with explanatory comments.
- There's a fine line between comments that illuminate and comments that obscure.
- Are the comments necessary?
- Do they need to be maintained?
- Do they explain "why" and not "what"?
- Can you refactor the code so the comments aren't required?
- And remember, you're writing comments for people, not machines.
- Problem
  - Created when code isn’t intuitive or obvious, but this masks a smell, which could be dealt with there and then
  - Some authors write comments as they lack the understanding of their audience, and write too much and which does not help the reader
  - Comments does get out of date, and when it does it confuses future readers
  - this includes console print statements
- Benefits
  - Code becomes more intuitive and obvious.
  - Less clutter
- Solution
  - The best comment is a good name for a method or class.
- Refactorings
  - If a comment is intended to explain a complex expression, the expression should be split into understandable subexpressions using Extract Variable.
  - If a comment explains a section of code, this section can be turned into a separate method via Extract Method. The name of the new method can be taken from the comment text itself, most likely.
  - If a method has already been extracted, but comments are still necessary to explain what the method does, give the method a self-explanatory name. Use Rename Method for this.
  - If you need to assert rules about a state that’s necessary for the system to work, use Introduce Assertion.
  - Write tests that document the commented code
- Trade off
  - Comments are necessary for certain things
    - Explain why this decision to code something, and not to refactor
    - For libraries
    - As a reminder, temp comment, to write actions/todo in code that you will come back to do while working on a feature and dont lose train of thought. These will be removed when actioned

#### Long Method

- problem
  - something is always being added to a method but nothing is ever taken out.
  - unnoticed until it becomes too late
  - Easier to add something and then forget about it
  - Reluctance to create new methods, due to difficulty (naming/what to extract) or size  of code to move (only a few lines)
- Benefits
  - All other things being equal, a shorter method is easier to read, easier to understand, and easier to troubleshoot.
  - Shorter methods, remove chance of unwatned and duplicated code
- Performance
  - negilble
  - Allows user to find specific areas faster and improve, with clearer understanding of code
- Solution
  - if you feel the need to comment on something inside a method, you should take this code and put it in a new method
    - single lines can and should be split off into a separate method, if it requires explanations.
  - Aim should be the method name should be descriptive enough with out looking inside
  - Refactor long methods into smaller methods if you can.
- Refactorings to use
  - To reduce the length of a method body, use Extract Method.
  - If local variables and parameters interfere with extracting a method, use
    - Replace Temp with Query
    - Introduce Parameter Object
    - Preserve Whole Object
  - If none of the previous recipes help, try moving the entire method to a separate object via Replace Method with Method Object
  - Conditional operators and loops are a good clue that code can be moved to a separate method.
    - For conditionals, use Decompose Conditional
    - If loops are in the way, try Extract Method

#### Long Parameter List

- Signs
  - More than three or four parameters for a method
- Problem
  - The more parameters a method has, the more complex it is.
  - Occur after merging several methods
  - be the byproduct of efforts to make classes more independent of each other.
  - It’s hard to understand such lists, which become contradictory and hard to use as they grow longer
  - The method is not in the correct class, as it needs infromation (param list) from another class
- Benefits
  - More readable, shorter code.
  - Refactoring may reveal previously unnoticed duplicate code
- refactoring
  - Limit the number of parameters you need in a given method, or use an object to combine the parameters.
  - Check what values are passed to parameters. If some of the arguments are just results of method calls of another object, use Replace Parameter with Method Call.
    - This object can be placed in the field of its own class or passed as a method parameter.
  - Instead of passing a group of data received from another object as parameters, pass the object itself to the method, by using Preserve Whole Object.
  - If there are several unrelated data elements, sometimes you can merge them into a single parameter object via Introduce Parameter Object.
- Avoid
  - cause unwanted dependency between classes
- Trade off
  - Can create intermediate objects to bundle all the params, but this leads to increas in anemic objects
  - May want to pass specific params, instead of an object containing all the params or that includes all params and other stuff.
    - This can make understanding the method better

#### Duplicated code

	- signs
		- copy and pasted code
		- similar code spread throughout class or files
		- Mulitple developers working on same file code (main branch/vertical arch)
		- IDE will point it out and suggest fix
		- Code which are different, but do the samething
	- Problem
		- Duplicated work
		- changes in one area means changes to others, sometimes no warning if this needs to happen
		- More code to maintain
	- Avoid
		- Time, better to duplicate and fix, then spend time and lose money
			- will need to fix later on (tech debt)
		- If duplicated once, its generally fine, but more than twice should look to refactor
		- Removing duplication can lead to more complex and abstract code which may not be worth it
	- Benefits
		- Merging duplicate code simplifies the structure of your code and makes it shorter.
		- Simplification + shortness = code that’s easier to simplify and cheaper to support.
	- Refactoring
		- If the same code is found in two or more methods in the same class: use `Extract Method` and place calls for the new method in both places.
		- If the same code is found in two subclasses of the same level:
			- Use `Extract Method` for both classes, followed by `Pull Up Field` for the fields used in the method that you’re pulling up.
			- If the duplicate code is inside a constructor, use `Pull Up Constructor Body`.
			- If the duplicate code is similar but not completely identical, use `Form Template Method`.
			- If two methods do the same thing but use different algorithms, select the best algorithm and apply `Substitute Algorithm`.
		- If duplicate code is found in two different classes:
			- If the classes aren’t part of a hierarchy, use `Extract Superclass` in order to create a single superclass for these classes that maintains all the previous functionality.
			- If it’s difficult or impossible to create a superclass, use `Extract Class` in one class and use the new component in the other.
		- If a large number of conditional expressions are present and perform the same code (differing only in their conditions), merge these operators into a single condition using C`onsolidate Conditional Expression` and use `Extract Method` to place the condition in a separate method with an easy-to-understand name.
		- If the same code is performed in all branches of a conditional expression: place the identical code outside of the condition tree by using `Consolidate Duplicate Conditional Fragments`.
  - Duplicated code is the bane of software development.
  - Stamp out duplication whenever possible.
  - You should always be on the lookout for more subtle cases of near-duplication, too
    - Change to make exact duplication, then extract out


#### Conditional Complexity
  - 	Watch out for large conditional logic blocks, particularly blocks that tend to grow larger or change significantly over time.
  - Consider alternative object-oriented approaches such as decorator, strategy, or state.
#### Combinatorial Explosion
  - You have lots of code that does almost the same thing.. but with tiny variations in data or behavior.
  - This can be difficult to refactor-- perhaps using generics or an interpreter

#### Large Class

- Large classes, like long methods, are difficult to read, understand, and troubleshoot.
- Does the class contain too many responsibilities?
- Can the large class be restructured or broken into smaller classes?
- Signs
	- A class contains many fields/methods/lines of code
- How it happens
	- Over time, class is added to with out refactoring
	- Less taxing to add to a method, then split apart
- Benefits
	- reduces developers from needing to remember a large number of attributes for a class
	- splitting large classes into parts avoids duplication of code and functionality
- Refactoring
	- if part of the behavior of the large class can be spun off into a separate component, use `Extract Class`
	-  if part of the behavior of the large class can be implemented in different ways or is used in rare cases, use `Extract Subclass`
	-  if it’s necessary to have a list of the operations and behaviors that the client can use `Extract Interface`
	- If a large class is responsible for the graphical interface, you may try to move some of its data and behavior to a separate domain object. In doing so, it may be necessary to store copies of some data in two places and keep the data consistent, use `Duplicate Observed Data`
-

#### Mysterious Name
	- The name that we use is not clear or meaningful or how to use it, that leads us to investigate (ie go through logic of code)
	- Applies to functions, modules, variables, classes
	- Naming should be given a lot of thought to
	- Also applies to the signature
	- Refactorings to use
		- Change Function Declaration (to rename a function)
		- Rename Variable
		- Rename Field

#### Type Embedded in Name
  - Avoid placing types in method names;
  - it's not only redundant, but it forces you to change the name if the type changes.
    - coupling between method/variable and naming
#### Uncommunicative Name
  - Does the name of the method succinctly describe what that method does?
  - Could you read the method's name to another developer and have them explain to you what it does?
  - If not, rename it or rewrite it.
#### Inconsistent Names
  - Pick a set of standard terminology and stick to it throughout your methods.
  -  For example, if you have Open(), you should probably have Close().

####  Dead Code

-  Ruthlessly delete code that isn't being used.
-  That's why we have source control systems!
- Signs
	- A variable, parameter, field, method or class is no longer used
- How it happens
	- Change in requirements or corrections made, and nobody had time to clean up the old code
	- Such code could also be found in complex conditionals, when one of the branches becomes unreachable (due to error or other circumstances)
	- Keeping code around just in case, instead of relying on version control
- Refactoring
	- Use the IDE
	- Delete unused code and unneeded files
	- In the case of an unnecessary class, `Inline Class` or `Collapse Hierarchy` can be applied if a subclass or superclass is used
	- To remove unneeded parameters, use `Remove Parameter`

####  Speculative Generality

-  Write code to solve today's problems, and worry about tomorrow's problems when they actually materialize.
-  YAGNI
-  signs
	-

####  Oddball Solution
  -  There should only be one way of solving the same problem in your code.
  -  If you find an oddball solution, it could be a case of poorly duplicated code-- or it could be an argument for the adapter model,
    -  if you really need multiple solutions to the same problem.

####  Temporary Field

- Watch out for objects that contain a lot of optional or unnecessary fields.
-  If you're passing an object as a parameter to a method, make sure that you're using all of it and not cherry-picking single fields.
-  a case in which a variable is in the class scope, when it should be in method scope. This violates the information hiding principle.
- Signs
	- Temporary fields get their values (and thus are needed by objects) only under certain circumstances. Outside of these circumstances, they’re empty.
- How it happens
	- temporary fields are created for use in an algorithm that requires a large amount of inputs. So instead of creating a large number of parameters in the method, the programmer decides to create fields for this data in the class. These fields are used only in the algorithm and go unused the rest of the Time
	- This kind of code is tough to understand. You expect to see data in object fields but for some reason they’re almost always empty.
- Refactoring
	- Temporary fields and all code operating on them can be put in a separate class via `Extract Class`.
		-  you’re creating a method object, achieving the same result as if you would perform `Replace Method with Method Object`
	-  `Introduce Null Object` and integrate it in place of the conditional code which was used to check the temporary field values for existence

#### Switch Statements

- Signs
	- There exists a complex switch operator or sequence of if statements
- How it happens
	- Relatively rare use of switch and case operators is one of the hallmarks of object-oriented code.
	- If there are multiple switch or if/else code duplicated, then need to change
	- Logical conditions are constantly added making it confusing
- Benefits
	- Use of polymorphism to make code simpler
	- Code is more organised
- Avoid
	- When a switch operator performs simple actions, there’s no reason to make code changes
	- Often switch operators are used by factory design patterns (Factory Method or Abstract Factory) to select a created class
- Refactoring
	- To isolate switch and put it in the right class, you may need `Extract Method` and then `Move Method`
	- If a switch is based on type code, such as when the program’s runtime mode is switched, use `Replace Type Code with Subclasses` or `Replace Type Code with State/Strategy`
	- After specifying the inheritance structure, use `Replace Conditional with Polymorphism`
	- If there aren’t too many conditions in the operator and they all call same method with different parameters, polymorphism will be superfluous.
		- If this case, you can break that method into multiple smaller methods with `Replace Parameter with Explicit Methods` and change the switch accordingly
	- If one of the conditional options is null, use `Introduce Null Object`

#### Loops

- Use a language or library which helps avoid using loops
- Refactoring
	- Replace Loop with Pipeline
		- With first ­class functions this can be implemented (ie streams)
		- help us quickly see the elements that are included in the processing and what is done with them

### Code Smells Between Classes

#### Alternative Classes with Different Interfaces

- If two classes are similar on the inside, but different on the outside, perhaps they can be modified to share a common interface.
- Signs
	- Two classes perform identical functions but have different method names
- How it happens
	- The programmer who created one of the classes probably didn’t know that a functionally equivalent class already existed
	- Copy and paste
- Benefits
	- Remove duplicated code, less code
	- more readable and understandable
- Refactoring
	- `Rename Method`s to make them identical in all alternative classes
	- `Move Method`, `Add Parameter` and `Parameterize Method` to make the signature and implementation of methods the same.
	- If only part of the functionality of the classes is duplicated, use ` Extract Superclass`, where exisiting class becomes subclass
	- When functions are the same, inject the class into classes that use it
	- When done can delete
- Avoid
	- Sometimes merging classes is impossible or so difficult as to be pointless

#### Primitive Obsession

- Don't use a gaggle of primitive data type variables as a poor man's substitute for a class. If your data type is sufficiently complex, write a class to represent it.
- Primitive Obsession is actually more of a symptom that causes bloats than a bloat itself. When a Primitive Obsession exists, there are no small classes for small entities (e.g. phone numbers). Thus, the functionality is added to some other class, which increases the class and method size in the software
- signs
	- Use of primitives instead of small objects for simple tasks (
		- such as currency, ranges, special strings for phone numbers, etc
	- Use of constants for coding information
		- such as a constant USER_ADMIN_ROLE = 1 for referring to users with administrator rights
	- Use of string constants as field names for use in data arrays
- How it happens
	- Creating a field or variable for some type, instead of a new class, then more primitive fields were added that related to the same idea was added instead of being put/encapsulated into a class
	- Primitives are often used to “simulate” types
		- instead of a separate data type, you have a set of numbers or strings that form the list of allowable values for some entity. Easy-to-understand names are then given to these specific numbers and strings via constants, which is why they’re spread wide and far.
	- Field simulation
		- The class contains a large array of diverse data and string constants (which are specified in the class) are used as array indices for getting this data.
- Benefits
	- More flexible code
	- Better understandability and organization of code. Operations on particular data are in the same place, instead of being scattered. No more guessing about the reason for all these strange constants and why they’re in an array
	- Easier finding of duplicate code
	- Using types instead of primitives, prevents using wrong value in method arguments
		- ie SomeObject.method("Boo", "Foo") vs SomeObject.method(new Boo("Boo"), new Foo("Foo"))
	- Domain language is encapsulated and forced to use where they are meant to
- Refactoring
	- `Replace Data Value with Object`
		- If you have a large variety of primitive fields, it may be possible to logically group some of them into their own class.
		- Even better, move the behavior associated with this data into the class too
	- If the values of primitive fields are used in method parameters, go with `Introduce Parameter Object` or `Preserve Whole Object`
	- When complicated data is coded in variables, use
		- `Replace Type Code with Class`
		- `Replace Type Code with Subclasses` or
		- `Replace Type Code with State/Strategy`
	- If there are arrays among the variables, use `Replace Array with Object`

#### Data Class

- Avoid classes that passively store data.
- Classes should contain data and methods to operate on that data, too.
- Signs
	- a class that contains only fields and crude methods for accessing them (getters and setters).
	- don’t contain any additional functionality and can’t independently operate on the data that they own.
	- logic concerned to those classes are treated in separate classes when could be done in the same class.
- Refactoring
	- If a class contains public fields, use `Encapsulate Field` to hide them from direct access and require that access be performed via getters and setters only
	- Use `Encapsulate Collection` for data stored in collections (such as arrays)
		- First class data structures
	- Review the client code that uses the class. In it, you may find functionality that would be better located in the data class itself. If this is the case, use `Move Method` and `Extract Method` to migrate this functionality to the data class.
	- After the class has been filled with well thought-out methods, you may want to get rid of old methods for data access that give overly broad access to the class data. Use `Remove Setting Method` and `Hide Method`
- Benefits
	- Operations on particular data are now gathered in a single place, instead of haphazardly throughout the code.
- Reasons against
	- Demanded by framework to have data classes (DAO)
	- Want to separate out the classes used in different layers (DTO)
	- This will not work if you want to use functional style, you need immutable objects that means the objects should not be changed, and data objects allows this.
		- Helps with multi threading
	- pure data objects can be invaluable for modeling relationships, validation, controlling access/changes
- Links
	- https://www.reddit.com/r/csharp/comments/bg6mhf/data_class_is_it_really_a_smell/


#### Data Clumps

- If you always see the same data hanging around together, maybe it belongs together.
- With Data Clumps there exists a set of primitives that always appear together (e.g. 3 integers for RGB colors). Since these data items are not encapsulated in a class this increases the sizes of methods and classes.
- Consider rolling the related data up into a larger class.
- Signs
	- different parts of the code contain identical groups of variables (such as parameters for connecting to a database). These clumps should be turned into their own classes
- How it happens
	- poor program structure
	- copy and paste
- How to spot
	- delete one of the data values and see whether the other values still make sense. If this isn’t the case, this is a good sign that this group of variables should be combined into an object
- Benefits
	- Improves understanding and organization of code. Operations on particular data are now gathered in a single place, instead of haphazardly throughout the code
	- Reduces code size
- Refactoring
	- If repeating data comprises the fields of a class, use `Extract Class` to move the fields to their own class.
	- If the same data clumps are passed in the parameters of methods, use `Introduce Parameter Object` to set them off as a class
	- If some of the data is passed to other methods, think about passing the entire data object to the method instead of just individual fields. Use `Preserve Whole Object`
	- Look at the code used by these fields or parameter. It may be a good idea to move this code to a data class
- Drawbacks
	- passing the whole object, may cause an undesirable dependency between the two classes

#### Refused Bequest

- If you inherit from a class, but never use any of the inherited functionality, should you really be using inheritance?
- Signs
	- If a subclass uses only some of the methods and properties inherited from its parents, the hierarchy is off-kilter. The unneeded methods may simply go unused or be redefined and give off exceptions
- How it happens
	- USe of inheritance between classes only by the desire to reuse the code in a superclass. But the superclass and subclass are completely different.
- Benefits
	- Makes code clear
- Refactoring
	- If inheritance makes no sense and the subclass really does have nothing in common with the superclass, eliminate inheritance in favor of `Replace Inheritance with Delegation`
	- If inheritance is appropriate, get rid of unneeded fields and methods in the subclass. Extract all fields and methods needed by the subclass from the parent class, put them in a new subclass, and set both classes to inherit from it. Use `Extract Superclass`


#### Inappropriate Intimacy

- Watch out for classes that spend too much time together, or classes that interface in inappropriate ways.
- that two classes are coupled tightly to each other
- Classes should know as little as possible about each other.
- Signs
	- One class uses the internal fields and methods of another class
- How this happens
	- Keep a close eye on classes that spend too much time together. Good classes should know as little about each other as possible. Such classes are easier to maintain and reuse
- Refactoring
	- The simplest solution is to use `Move Method` and `Move Field` to move parts of one class to the class in which those parts are used. But this works only if the first class truly doesn’t need these parts
	- use `Extract Class` and `Hide Delegate` on the class to make the code relations “official”
	- If the classes are mutually interdependent, you should use `Change Bidirectional Association to Unidirectional`
	- If this “intimacy” is between a subclass and the superclass, consider `Replace Delegation with Inheritance`

#### Indecent Exposure
  - Beware of classes that unnecessarily expose their internals.
  - Aggressively refactor classes to minimize their public surface.
  - You should have a compelling reason for every item you make public.
    - If you don't, hide it.

#### Feature Envy

- Methods that make extensive use of another class may belong in another class.
- a case where one method is too interested in other classes
- Consider moving this method to the class it is so envious of.
- Signs
	- A method accesses the data of another object more than its own data.
- How it happens
	- may occur after fields are moved to a data class. If this is the case, you may want to move the operations on data to this class as well.
- Refactoring
	- if things change at the same time, you should keep them in the same place
	- If a method clearly should be moved to another place, use `Move Method`
	- If only part of a method accesses the data of another object, use `Extract Method` to move the part in question
	- If a method uses functions from several other classes, first determine which class contains most of the data used. Then place the method in this class along with the other data.
		- Alternatively, use `Extract Method` to split the method into several parts that can be placed in different places in different classes
- AVoid
	- Sometimes behavior is purposefully kept separate from the class that holds the data. The usual advantage of this is the ability to dynamically change the behavior
		- strategy, visitor patterns

#### Lazy Class

- Classes should pull their weight. Every additional class increases the complexity of a project.
- If you have a class that isn't doing enough to pay for itself, can it be collapsed or combined into another class?
- Signs
	- Understanding and maintaining classes always costs time and money. So if a class doesn’t do enough to earn your attention, it should be deleted
- How it happens
	- perhaps it was designed to support future development work that never got done.
	- Perhaps a class was designed to be fully functional but after some of the refactoring it has become ridiculously small
- Refactoring
	- Components that are near-useless, use `Inline Class`
	- For subclasses with few functions, use `Collapse Hierarchy`
- Avoid
	- Sometimes a Lazy Class is created in order to delineate intentions for future development, In this case, try to maintain a balance between clarity and simplicity in your code

#### Middle Man

- If a class is delegating all its work, why does it exist?
- Cut out the middleman.
- Beware classes that are merely wrappers over other classes or existing functionality in the framework.
- represent a problem that might be created when trying to avoid high coupling with constant delegation. Middle Man is a class that is doing too much simple delegation instead of really contributing to the application.
- Signs
	- If a class performs only one action, delegating work to another class, why does it exist at all?
- How this happens
	- This smell can be the result of overzealous elimination of Message Chains.
	- it can be the result of the useful work of a class being gradually moved to other classes. The class remains as an empty shell that doesn’t do anything other than delegate.
- Refactoring
	- If most of a method’s classes delegate to another class, Remove Middle Man is in order
- Avoid
	- A middle man may have been added to avoid interclass dependencies.
	- Some design patterns create middle man on purpose (such as Proxy or Decorator)

#### Message Chains

- Watch out for long sequences of method calls or temporary variables to get routine data.
- Intermediaries are dependencies in disguise.
- is a smell where class A needs data from class D.
- To access this data, class A needs to retrieve object C from object B (A and B have a direct reference). When class A gets object C it then asks C to get object D. When class A finally has a reference to class D, A asks D for the data it needs.
- The problem here is that A becomes unnecessarily coupled to classes B, C, and D, when it only needs some piece of data from class D.
- The following example illustrates the message chain smell: A.getB().getC().getD().getTheNeededData()
- Signs
	- In code you see a series of calls resembling A.getB().getC().getD().getTheNeededData()
- How this happens
	- A message chain occurs when a client requests another object, that object requests yet another one, and so on. These chains mean that the client is dependent on navigation along the class structure. Any changes in these relationships require modifying the client
- Refactoring
	- To delete a message chain, use `Hide Delegate`
	- Sometimes it’s better to think of why the end object is being used. Perhaps it would make sense to use `Extract Method` for this functionality and move it to the beginning of the chain, by using `Move Method`
- Avoid
	- Overly aggressive delegate hiding can cause code in which it’s hard to see where the functionality is actually occurring. Which is another way of saying, avoid the Middle Man smell as wel

#### Divergent Change

- If, over time, you make changes to a class that touch completely different parts of the class, it may contain too much unrelated functionality.
- Consider isolating the parts that changed in another class.
- Divergent Change is when many changes are made to a single class.
- Signs
	- having to change many unrelated methods when you make changes to a class
	-  For example, when adding a new product type you have to change the methods for finding, displaying, and ordering products.
- Benefits
	- Improves code organization
	- Reduces code duplication
	- Simplifies support
-  How this happens
	-  poor program structure
	-  copy paste
-  Refactoring
	- Split up the behavior of the class via `Extract Class`
	- If different classes have the same behavior, you may want to combine the classes through inheritance, use `Extract Superclass` and `Extract Subclass`


#### Shotgun Surgery

- If a change in one class requires cascading changes in several related classes, consider refactoring so that the changes are limited to a single class.
- Shotgun Surgery refers to when a single change is made to multiple classes simultaneously.
- How this happens
	- A single responsibility has been split up among a large number of classes. This can happen after overzealous application of `Divergent Change`
- Refactoring
	- Use `Move Method` and `Move Field` to move existing class behaviors into a single class. If there’s no class appropriate for this, create a new one.
	- If moving code to the same class leaves the original classes almost empty, try to get rid of these now-redundant classes via `Inline Class`.
- Benefits
	- easier maintance

#### Parallel Inheritance Hierarchies

- Every time you make a subclass of one class, you must also make a subclass of another.
- Consider folding the hierarchy into a single class.
- Signs
	- Whenever you create a subclass for a class, you find yourself needing to create a subclass for another class
- How this happens
	- Inheritence hierarchy grew too large
- Refactorign
	- You may de-duplicate parallel class hierarchies in two steps.
		- First, make instances of one hierarchy refer to instances of another hierarchy.
		- Then, remove the hierarchy in the referred class, by using `Move Method` and `Move Field`
- Avoid
	- Sometimes having parallel class hierarchies is just a way to avoid even bigger mess with program architecture. If you find that your attempts to de-duplicate hierarchies produce even uglier code, just step out, revert all of your changes and get used to that code.

#### Incomplete Library Class

- We need a method that's missing from the library, but we're unwilling or unable to change the library to include the method. The method ends up tacked on to some other class.
- If you can't modify the library, consider isolating the method.
- Signs
	- Sooner or later, libraries stop meeting user needs. The only solution to the problem—changing the library—is often impossible since the library is read-only.
- How this happens
	- The author of the library hasn’t provided the features you need or has refused to implement them
- Refactoring
	- To introduce a few methods to a library class, use `Introduce Foreign Method`
	- For big changes in a class library, use `Introduce Local Extension`
- Benefit
	- instead of creating your own library from scratch, you can still piggy-back off an existing one
- Linke
	- https://www.youtube.com/watch?v=XkrtVVbDIEU


#### Solution Sprawl
  - If it takes five classes to do anything useful, you might have solution sprawl.
  - Consider simplifying and consolidating your design.

#### Global Data

- global data is that it can be modified from anywhere in the code base, and there’s no mechanism to discover which bit of code touched it
- most obvious form of global data is global variables, but we also see this problem with class variables and singletons.
- Refactorings
	- Encapsulate Variable
		- when you have it wrapped by a function, you can start seeing where it’s modified and start to control its access
		- Then, it’s good to limit its scope as much as possible by moving it within a class or module where only that module’s code can see it
	- Enforce immutability
- Global data is especially nasty when it’s mutable.

#### Mutable Data

- Changes to data can often lead to unexpected consequences and tricky bugs.
	- I can update some data here, not realizing that another part of the software expects something different and now fails—a failure that’s particularly hard to spot if it only happens under rare conditions
- Mutable data isn’t a big problem when it’s a variable whose scope is just a couple of lines
- Refactoring
	- Use functional programming
		- use immutable data
		- When updating data, return new copy of data
		- use language that enforces this or write tests
	-  Encapsulate Variable
		-  to ensure that all updates occur through narrow functions that can be easier to monitor and evolve
	-  Split Variable
		-  If a variable is being updatedto store different things
		-  to keep them separate and avoid the risky update
	-  Slide Statements
		-  move logic out of code that processes the update
	-  Extract Function
		-  to separate the side ­effect ­free code from anything that performs the update
	-  Separate Query from Modifier
		- to ensure callers don’t need to call code that has side effects unless they really need to
	- Remove Setting Method
		- trying to find clients of a setter helps spot opportunities to reduce the scope of a variable
	- Replace Derived Variable with Query
	- Combine Functions into Class or Combine Functions into Transform
		-  to limit how much code needs to update a variable.
	-  Change Reference to Value
		-  If a variable contains some data with internal structure, it’s usually better to replace the entire structure rather than modify it in place



## Bad Code Smells Taxonmy

- https://web.archive.org/web/20201218073012/http://mikamantyla.eu/BadCodeSmellsTaxonomy.html

### The Bloaters

- Contains:
  - Long Method
  - Large Class
  - Primitive Obsession
  - Long Parameter List
  - DataClumps
- Bloater smells represents something that has grown so large that it cannot be effectively handled.

### The Object-Orientation Abusers

- Contains:
  - Switch Statements
  - Temporary Field
  - Refused Bequest
  - Parallel Inheritance Hierarchies
  - Alternative Classes with Different Interfaces
- they represent cases where the solution does not fully exploit the possibilities of object-oriented design.
- Switch Statements
  - something that should be avoided in object-oriented programming. The situation where switch statements or type codes are needed should be handled by creating subclasses

### The Change Preventers
- Contains:
  - Divergent Change
  - Shotgun Surgery
  - Parallel Inheritance Hierarchies
- hinder changing or further developing the software
- violate the rule which says that classes and possible changes should have a one-to-one relationship.
  - For example, changes to the database only affect one class, while changes to calculation formulas only affect the other class.
- we have a single class that needs to be modified by many different types of changes
  - or many classes changes when making a single change

### The Dispensables
- Contains:
  - Lazy class
  - Data class
  - Duplicate Code
  - Dead Code,
  - Speculative Generality
- all represent something unnecessary that should be removed from the source code.
- contains two types of smells
  - dispensable classes
    - If a class is not doing enough it needs to be removed or its responsibility needs to be increased
  - dispensable code
    - Code that is not used or is redundant needs to be removed

### The Couplers

- Contains:
  - Feature Envy
  - Inappropriate Intimacy
  - Message Chains
  - Middle Man
- these increase coupling
-

## Links

- https://codurance.com/software-creation/2016/03/17/code-smells-part-I/
- https://codurance.com/software-craftsmanship/2016/05/07/code-smells-part-II/
- https://sourcemaking.com/refactoring/smells
- https://blog.codinghorror.com/code-smells/
- https://8thlight.com/blog/georgina-mcfadyen/2017/01/19/common-code-smells.html
- https://completedeveloperpodcast.com/episode-89/
- https://completedeveloperpodcast.com/episode-88/
- Sandi Metz https://www.youtube.com/watch?v=D4auWwMsEnY
- https://github.com/Droogans/unmaintainable-code
- https://gabrielfs7.github.io/design-principles/2019/09/24/code-smells/
-  [VDBUH2024] - Victor Rentea - Code Smells - Hall of Fame https://youtu.be/lsW0-sEGr3w?si=bua7cAAOYxm77Vab
