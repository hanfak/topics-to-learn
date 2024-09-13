# Aspect Oriented Programming

## What

-  helps in separating cross-cutting concerns from the main business logic
- Increased modularity is achieved by Aspects and they are configured to cut across different classes
-  aspects are used to inject additional behavior into your code without modifying the code itself.

### Definitions 

- Concerns (or cross cutting concerns)
  - These are functionalities that has to be added across multiple parts of program.
  - Example: Security, logging or error handling
    In our analogy, our concern is the security risk
- Aspects
    - a class that implements enterprise application concerns that cut across multiple classes
    - It is like master plan for dealing with concern. It encapsulate cross cutting concerns in a modular unit.
    - In our analogy, our plan to install CCTV in every room is aspects
- Join points
    -  a specific point in the application such as method execution, exception handling, changing object variable values, etc.
    - It is the specific points on our program where we want to apply the code
    - In our analogy , we were installing cctv in the room's entrance
- pointcuts
  -  is expressions that are matched with join points to determine whether advice needs to be executed or not
- Advice
    -  actions taken for a particular join point.
    -  methods that get executed when a certain join point with matching pointcut is reached in the application.
    - Advice is the actual code that implements our cross cutting concern and it is defined in join points
- Target Object
  -  the object on which advices are applied
  - Spring AOP is implemented using runtime proxies so this object is always a proxied object.
    - subclass is created at runtime where the target method is overridden and advice are included based on their configuration
- Weaving
  -  process of linking aspects with other objects to create the advised proxy objects.
  - This can be done at compile time, load time or at runtime
- Advice Types
  - Before Advice
    - These advices runs before the execution of join point methods.
  - After (finally) Advice
    - that gets executed after the join point method finishes executing, whether normally or by throwing an exception.
  - After Returning Advice
    -  advice methods to execute only if the join point method executes normally
  - After Throwing Advice
    - advice gets executed only when join point method throws exception, we can use it to rollback the transaction declaratively
  - Around Advice
    -  advice surrounds the join point method and we can also choose whether to execute the join point method or not.
    - write advice code that gets executed before and after the execution of the join point method
    - to invoke the join point method and return values if the method is returning something.

## Uses 

- Typical applications 
  - Data validations
  - logging
    - auditing
  - monitoring execution
  - retry mechanism
    - https://www.sivalabs.in/retrying-method-execution-using-spring-aop/
  - security
  - transaction management
    - https://www.marcobehler.com/guides/spring-transaction-management-transactional-in-depth
    - https://www.sivalabs.in/spring-boot-database-transaction-management-tutorial/
  - caching
    - https://trishagee.com/2008/04/14/aop_caching/
  - Exception handling
  - Performance monitoring
  - Read/write locks

## Examples 

- https://www.digitalocean.com/community/tutorials/spring-aop-example-tutorial-aspect-advice-pointcut-joinpoint-annotations
- https://www.baeldung.com/spring-aop
- https://docs.spring.io/spring-framework/docs/5.0.0.RELEASE/spring-framework-reference/core.html#aop
- 
    
## Advantages 

- Our application is more flexible and easy to manage,
- Getting rid of repetitive code patterns,
- A cleaner and more understandable code,
- Separation from core logic and intersections.


## Disadvantages

- Complexity
  - AOP can introduce additional complexity to a codebase. Understanding and debugging AOP aspects can be challenging for developers, especially those unfamiliar with the paradigm.
- Increased Learning Curve
  - Developers need to learn AOP concepts and tools, which can take time and effort.
- Overuse
  - Some developers may be tempted to use AOP for all aspects of a system, which can lead to an overcomplicated and hard-to-maintain codebase. It's essential to use AOP judiciously and only for cross-cutting concerns where it genuinely adds value.
- Misuse
  - Improper use of AOP can lead to scattering and tangling of aspects, resulting in a codebase that is even harder to maintain than before.
- Implicit Behaviour
  -  AOP can introduce behavior that is not explicitly visible in the business logic, making it harder for developers to understand what the code does by simply reading the business logic.
- Unexpected Interactions
  - can unintentionally affect the behavior of methods in ways that are not immediately apparent, leading to subtle bugs and side effects.
- Performance Overhead
  - Depending on how AOP is implemented, it can introduce some runtime performance overhead. This is particularly true for certain AOP frameworks that dynamically weave aspects into the code at runtime.
  - The additional layers of abstraction and the weaving process can increase memory and CPU usage.
- Framework Lock-In
  -  often ties you to a specific framework (such as Spring AOP or AspectJ), making it harder to switch to another framework or to use pure Java.
- Limited Language Support
  - Not all programming languages have robust AOP support, making it less accessible or practical in certain environments.
- Tooling and Ecosystem
  - The availability of AOP tools and libraries may vary depending on the programming language and framework you are using.
- Debugging Challenges
  - Debugging AOP code can be more complex than debugging traditional code, as aspects can affect multiple parts of the application.
  -  aspects can inject behavior into the code dynamically, it can be challenging to trace through the code during debugging. The flow of execution can be less predictable and harder to follow.
- Maintainability
  - Over time, AOP aspects can become difficult to maintain, especially if there are frequent changes to the main application code. Ensuring that aspects remain aligned with the evolving application can be challenging.
  - Aspects need to be maintained alongside the business logic. Changes in the core logic may necessitate changes in the aspects, and vice versa.
- Testing
  - Testing AOP aspects can be challenging, and it may require special testing strategies to ensure that aspects behave as expected.
- From the point of view of a programmer who's motto is "Keep It Simple Stupid", evaluating the usage of such models is dangerous. For what it attempts to accomplish, it renders a program far more difficult to comprehend and consequently easier to break.
- The genius of good programming is in its simplicity ironically. Complex programs might work, but are nightmares when it comes to maintenance, and when you consider that 2/3rds of time spent by a programmer is placed in fixing errors in programs, it doesn't pay off in the end.

### Links 
- https://stackoverflow.com/questions/875512/what-are-the-disadvantages-of-aspect-oriented-programming-aop
- https://www.scitepress.org/papers/2010/29216/29216.pdf
- https://www.jbktutorials.com/spring-aop/disadvantages-of-spring-aop.php#gsc.tab=0

## Alternatives

- Reflection
  - Create custom annotations that is used via reflection to add behaviour
-  you can encapsulate cross-cutting concerns into separate modules that are then used throughout the app via dependency injection. This allows you to somewhat decouple the cross-cutting concern implementation from it's use throughout the code.
- Decorator/proxy/template pattern
- Event listeners 
- Interceptors 
  - ie Spring  HandlerInterceptor for http requests
- Servlet Filters 

## Links

- https://en.wikipedia.org/wiki/Aspect-oriented_programming
- https://medium.com/@hinchman_amanda/introduction-to-java-aspect-oriented-programming-a9769613131e
