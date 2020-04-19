# Builder

## What

- pattern that lets you construct complex objects step by step. The pattern allows you to produce different types and representations of an object using the same construction code.

## Advantages

- Code is more maintainable if number of fields required to create object is more than 4 or 5.
- Object creational code less error-prone as user will know what they are passing because of explicit method call.
- Builder patter increses robustness, as only fully constructed object will be available to client.
- You can construct objects step-by-step, defer construction steps or run steps recursively.
- You can reuse the same construction code when building various representations of products.
-  You can isolate complex construction code from the business logic of the product.
- Immutable objects
- Self documentating creation of object

## Drawbacks

-  Builder pattern is verbose and requires code duplication as Builder needs to copy all fields from Original or Item class.
- It does not really guide the user through the creation.
- A user can always call the build method in any moment, even without the needed information.
- There is no way to guide the user from a creation path instead of another based on conditions.
- There is always the risk to leave your object in an inconsistent state.
  - You could also put default values around all the required properties, but then the readability of the code will be lost ( new PaninoBuilder().build(); what are you building here?)
- All methods are always available, leaving the responsibility of which to use and when to use to the user who did not write the api.

## when

- Use the Builder pattern to get rid of a “telescopic constructor”.
  - Say you have a constructor with ten optional parameters. Calling such a beast is very inconvenient; therefore, you overload the constructor and create several shorter versions with fewer parameters. These constructors still refer to the main one, passing some default values into any omitted parameters.
- Use the Builder pattern when you want your code to be able to create different representations of some product (for example, stone and wooden houses).
  -  The Builder pattern can be applied when construction of various representations of the product involves similar steps that differ only in the details.
  - The base builder interface defines all possible construction steps, and concrete builders implement these steps to construct particular representations of the product. Meanwhile, the director class guides the order of construction.
- Use the Builder to construct Composite trees or other complex objects.
  - The Builder pattern lets you construct products step-by-step. You could defer execution of some steps without breaking the final product. You can even call steps recursively, which comes in handy when you need to build an object tree.
  - A builder doesn’t expose the unfinished product while running construction steps. This prevents the client code from fetching an incomplete result.

## How

- Instead of making the desired object directly, the client calls a constructor (or static factory) with all of the required parameters and gets a builder object. Then the client calls methods on the builder object to set each optional parameters. Finally the client calls a build method which generate an instance of the object which is immutable.

## Difference between Builder and Abstract factory design pattern

- Abstract Factory emphasizes a family of product objects (either simple or complex).
  - Builder focuses on constructing a complex object step by step.
- Abstract Factory focus on what is made.
  - Builder focus on how it is made.
- Abstract Factory focus on defining many different types of factories to build many products, and it is not a one builder for just one product.
  - Builder focus on building a one complex but one single product.
- Abstract Factory defers the choice of what concrete type of object to make until run time.
  - Builder hide the logic/ operation of how to compile that complex object.
- In Abstract Factory, every method call creates and returns different objects.
  - In Builder, only the last method call returns the object, while other calls partially build the object

##  Relations with Other Patterns

- Many designs start by using Factory Method (less complicated and more customizable via subclasses) and evolve toward Abstract Factory, Prototype, or Builder (more flexible, but more complicated).
- You can use Builder when creating complex Composite trees because you can program its construction steps to work recursively.
- You can combine Builder with Bridge: the director class plays the role of the abstraction, while different builders act as implementations.
- Abstract Factories, Builders and Prototypes can all be implemented as Singletons.


## Links

- https://egkatzioura.com/2018/03/27/creational-design-patterns-builer-pattern/
- https://jaxenter.com/patterns-java-8-lambdas-127635.html
