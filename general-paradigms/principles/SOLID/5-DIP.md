# 5. Dependency Inversion Principle

-  reduce tight coupling
- The first that higher level code should not depend on lower level code, instead both high and low level code should depend on some abstraction
- the abstractions should not depend on the details, rather the other way around, that the details should depend on the abstractions.
- higher level code here represents the “what” or “workflow” with the lower level code performing specific actions as part of this workflow.
- Can use different implementations of the dependency
- DIP in conjunction with dependency injection also makes it possible to provide different concrete implementations of dependencies at runtime.
- Depend on the more-abstract thing

Why?
- Without DIP, the high level “workflow” is harder to separate from the implementation (in the lower level code).
- Classes are more tightly coupled, meaning that changes can ripple throughout the system
- it may make unit testing harder because fake versions of dependencies cannot easily be supplied
  - As newing objects occurs in the class under test

## Issues

- This is all about adding flexibility, codeing to the an interface
  - Taken to the extreme is bad
- This came about due to mocking frameworks needed interfaces, to be able to mock
  - Then adding final to the class, meant you could not mock it
- With all this dependency injection, you need a class/s in layer, that knows about all these dependenices, to be able to construct the object map
  - frameworks used to use xml config, now they use annotations, which make the code hard to follow

### Links
  - https://naildrivin5.com/blog/2019/12/02/dependency-inversion-principle-is-a-tradeoff.html

## In depth 

Yes, every program composed of o operations and t types has a complexity of oxt.

If we use OO we can increase t with minimum disruption to the source code; but increasing o disrupts many source code modules.
If we use switch statements we can increase o with minimum disruption to the source code; but increasing t disrupts many source code modules.

However, notice that the issue, in both cases, is source code management. It has nothing to do with the runtime execution. So let's split this problem into two issues: Run Time and Source Code.

Run Time

I propose a hypothetical compiler that produces identical binary code irrespective of whether the input is operand or operation primal. If you give this compiler OO source code S1, it will produce binary output B1. If you give this compiler procedural source code S2 it will produce binary output B2. So long as the behavior of the two programs is identical, then B1 and B2 are also, byte for byte, identical.

It should be clear that a compiler like this is possible since switch statements can be (and often are) compiled as jump tables; and polymorphic dispatches can be (and often are) compiled as jump tables.

Yes, there are complicating issues; but let's ignore them and agree that such a compiler is at least feasible.

Thus, since they can be compiled down into identical binary code, there is no necessary Run Time difference between the OO and Procedural styles.

Source Code

As we have already agreed the swapping of o and t makes very little difference to the problem of source file management. Individual cases may favor one style or another. For example if we have stable operations but variable types then OO might be favored. Or if we have stable types but variable operations then a Procedural style may be favored.

So it looks like, all else being equal, the two styles have the same capabilities. There is no Run Time difference, and the Source Code management issues are just mirrors of each other.

Dependency Inversion

But all else is not equal. There is a radical difference in the source file dependency structures created by the two styles.

Operation Primal: In the procedural style, in which switch (if/else) statements deploy operations over types, the source code dependencies (#include statements in C/C++) follow the Run Time dependencies. High level modules that call lower level modules must #include those lower level modules. So the #include chains form a Directed Acyclic Graph (DAG) in which every edge is directed from a higher level module to a lower level module and follows precisely the direction of the function calls. (Ignoring the .h .c divide which we can discuss at length later.)
Operand Primal: In the OO style, in which dynamic polymorphism is used to deploy types over operations, higher level modules are independent of lower level modules. The #include statements point in the opposite direction. Subtypes depend upon their base types. Thus the source code dependencies point against the runtime calls, against the flow of control. The edges of the #include DAG are directed from lower level modules towards higher level modules.
The implications of this difference are:

When using the procedural style high level policies depend, at compile time, upon low level details. If those low level details change for any reason, the high level policies must be recompiled and redeployed even though they have not changed in their intent.
When using the OO style high level policies are independent of low level details. If those details change in implementation, the high level modules remain unaffected. They do not need to be recompiled or redeployed.
Example

In the 1950s and 1960s we would write code that directly used the IO devices of the day. These devices were things like card readers and punches, paper tape readers and punches, teletypes, printers, and magnetic tape drives. If someone asked us to write a payroll application that took in employee data as punched cards and wrote paychecks on the line printer then our code would do exactly that. It would explicitly read from the card reader, and explicitly write to the line printer. We used the Operation Primal, procedural, style.

But then our customers would come to us one day and ask us to read the employee data from magnetic tape, and output the paycheck data to another magnetic tape. To them, this was a low leve detail. The data was still the same, it was just on a different medium. But to us it was a complete architectural rewrite. Magnetic tape drives are very different from card readers and line printers. And so the change was very expensive, and our clients could not understand why.

To defend against this we invented Device Independence. We created an abstraction called a File and gave it standard operations such as open, close, read, write, and seek. (The five standard functions of the UNIX IO driver). We categoried our IO devices as types. We used dynamic polymorphism (jump tables) to implement the dispatching. By creating a stable set of operations, we forced virtually all of the variation into the types -- the different IO drivers.

From then on, we could write our applications without knowing, or caring what IO devices we were using. And life become a lot simpler for the programmer at large, and a lot less expensive for clients who made "small" changes to the media they wanted to use. Those changes were made in the job control directives without forcing any source code change, recompilation, or redeployment of the application.

But wait...

You could easily make the point that while the OO style protects high level policy from changes to low level detail, it also makes low level detail vulnerable to changes in high level policy. That's true. And by the same token, the procedural style certainly makes high level policy vulnerable to changes in low level details, but protects those low level details from changes to the high level policies.

So the question then becomes one of architectural philosophy: Which of those two is more likely to change? Does policy change more frequently than detail? Or does detail change more frequently than policy?

## Links

- https://dzone.com/articles/solid-design-principles-explained-dependency-inver
- https://dzone.com/articles/solid-principles-dependency-inversion-principle
- https://stackify.com/dependency-inversion-principle/
