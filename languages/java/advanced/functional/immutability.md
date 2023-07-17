# Immutability

## Classes

- This depends on design decisions
- By using "final" in class signature, you cannot sub class it
- Make constructor private, use static factory methods
  - If constructor is non default, create a new default private constructor and throw an ```AssertionException("should not instantiate this class")```. This avoids reflection being used to create an instance
- https://stackoverflow.com/questions/12306651/why-would-one-declare-an-immutable-class-final-in-java
## Fields

- Use of private final fields
- No setter methods
- Methods that change the state, should be avoided
  - instead return a new object with the new state in constructor
- But if you have access to the fields via a getter, then the object can stil be mutated internally
  - Thus getter has to either return a copy (deep or shallow copy depending on the object graph)

## Arguments

- Either by convention (to avoid cluttering code), keep all method parameters final.
- Can use the keyword "final" in method parameters signature
- Even better would be to make any argument passed into a method be immutable
  - This can be hard, and also lead to trade off in creating less readable code

## Variables

### Assign once

- Bad
```java
Thing thing;
if (nextToken == MakeIt) {
  thing = makeTheThing();
} else {
  thing = new SpecialThing(dependencies);
}
thing.doSomethingUseful();
```
- Better, use ternary and assign to variable
```java
final var thing =
  nextToken == MakeIt ? makeTheThing(): new SpecialThing(dependencies);
thing.doSomething();
```
- Better, wrap it in a function
```java
final var thing = aThingFor(nextToken);
thing.doSomethingUseful();

private Thing aThingFor(Token aToken) {
  return aToken == MakeIt ? makeTheThing() : new SpecialThing(dependencies);
}
```
- If used once, can inline, and get rid of variable (as long naming of method is good)
```java
aThingFor(nextToken).doSomethingUseful();

private Thing aThingFor(Token aToken) {
  return aToken == MakeIt ? makeTheThing() : new SpecialThing(dependencies);
}
```
- For complex conditions, like switches, can wrap it up in a method

### Localise scope

- Distance between assigning variable and use is far apart
```java
var thing = Thing.DEFAULT;
// lots of code to figure out nextToken
if (nextToken == MakeIt) {
  thing = makeTheThing();
}
thing.doSomethingUseful();
```
- Better, use private method
```java
final var thing = theNextThingFrom(aStream);

private Thing theNextThingFrom(Stream aStream) {
// lots of code to figure out nextToken
  if (nextToken == MakeIt) {
    return makeTheThing();
  }
  return Thing.DEFAULT;
}
```
- Better use stream
```java
final var thing = nextTokenFrom(aStream)
                    .filter(t -> t == MakeIt)
                    .findFirst()
                    .map(t -> makeTheThing())
                    .orElse(Thing.DEFAULT);
```
