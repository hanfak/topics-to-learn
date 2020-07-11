# reflection

- Most frameworks are built on reflection (spring/jakarta)
- Android (dagger DI framework) and micronaut dont use reflection

## Links

- http://www.java2s.com/Tutorials/Java/Java_Reflection/index.htm
- http://tutorials.jenkov.com/java-reflection/index.html
- https://www.javacodegeeks.com/2018/01/java-reflection-much-faster.html
- https://www.javatpoint.com/java-reflection

## Drawbacks

- Don't use if you want low memory comsumption
- It is relatively slow
- Because there is no common reflection cache in Java, and reading reflective data is expensive, each library and framework produces a unique reflection cache. In a typical modern Java application, you will find Spring has a unique cache, Groovy has another cache, Jackson another, and so on. This makes it extremely difficult to optimize memory consumption.
- Reflective calls are much more difficult for the JIT to optimize. Efforts such as InvokeDynamic and others try to alleviate this situation, but reflective calls will never be as efficient.
-

- https://softwareengineering.stackexchange.com/questions/101187/are-there-problems-with-using-reflection
-
