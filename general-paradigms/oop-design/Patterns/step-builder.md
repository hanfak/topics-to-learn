# Step Builder Pattern

## What

- An improvement on the builder pattern
- If the builder is used, but the creation of the object needs to done in a ordered way or certain state needs to be set before instantiation the step builder overcomes these problems that tthe builder pattern has.

## How

- Write creational steps inner classes or interfaces where each method knows what can be displayed next.
- Implement all your steps interfaces in an inner static class.
- Last step is the BuildStep, in charge of creating the object you need to build.

## Advantages

- User guidance for your API through the object creation process step by step.
- API User can call the builder's build() method once the object is in a consistent state.
- Reduced opportunity for the creation of inconsistent object instances.
- Sequencing initialization of mandatory fields.
- Fluent API.
- No need for providing validate() method for field validation.

## Drawbacks

- It should be used with cautions and only if your API is composed of small objects that do not change.
- Low readability of code needed to implement the pattern itself.

## When

- Use the Step Builder pattern when the algorithm for creating a complex object should be independent of the parts that make up the object and how they're assembled the construction process must allow different representations for the object that's constructed when in the process of constructing the order is important.
