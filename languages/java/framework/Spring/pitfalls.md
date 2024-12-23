# Pitfalls and advice

- it provides too many things as a single dependency, which has caused a lot of pain over the years because teams that used it just for dependency injection needed to constantly update it for security issues non-related to any dependency injection feature, which is the opposite of Guice and Dagger
- slows down your app’s startup time
- You won’t find out if your app works or not, until you run it - in large commercial environments it can mean up to an hour build and deployment time
  - then you get a massive stacktrace, half of which concerns internal spring classes
- Once you go beyond a simple singleton wiring scenario, Spring can get very ugly, very flaky and unpredictable
- It helps you start, but the further you go, the more of a maintenance nightmare it becomes.
- when a project use Spring beyond its DI features it becomes extremely coupled to Spring and then it’s architected based on the framework capabilities and not the business logic
- Requires configuration
  - either xml, which makes it hard to use or debug
    - so bad they changed to using annotations
    - but still code bases using this, wiht poor documentation and help/expertise
  - annotations, whihc leads to magic
    - you lose compile time checking and the ability of things to blow up at runtime when using Spring is less than idea
- Deep learning curve
- it tries to be all things to all (Java) programmers it’s not necessarily the best at any one of them
  - Due to being able to do so many things, Spring kind of messes with the simplicity benefits we get from using Java.
    - Spring discreetly introduces complexity to your project, the framework is simple on the surface, when it works, but not many people can explain what is happening under the hood in Spring
- Debugging Spring errors often seems like black magic, it’s 90% guess work and pattern matching.
  - Poor or outdated documentation  does not help
- Spring is opinionated and tends to infect your codebase quite quickly. It is difficult to constrain Spring to certain modules, Spring can quickly becomes a core component of your architecture
  - coupling the framework to the app, which is not great
- Spring is a very heavyweight framework, the Spring dependencies alone are often orders of magnitude larger than your applications, even if you just want to use the simplest functionality.
- Dependency management
  - spring pulls in a lot of dependencies which can clash with other libraries you use
- Spring can often save you weeks of work at the beginning of a project, you may feel you are getting these benefits for free, you aren’t
  - but the complexity and technical debt hits you at a much later stage.
  - similar to using dynamic languages
- Spring is essentially a band aid on top of the limitations of the Java language
- Conventions may be common, but they are not frequently universal. If someone comes in who does not understand these conventions, it can really make things difficult to figure out. Somehow things just seem to work and there's no clear reason why. And when things don't work, it can be really difficult to figure out why.
- Forces developers to learn and understand (ableit at a surface level) the spring dsl, rather than how to code
  - ie instead of new up a class with some code,they will bring up a spring app
- people who have worked with Spring in the past tend to use it everywhere they can, without thinking too much
- Use of annotations
  - hard to manipulate and debug
  - https://blog.softwaremill.com/the-case-against-annotations-4b2fb170ed67

## Links

- https://dzone.com/articles/spring-pitfalls-proxying
- https://www.toptal.com/spring/top-10-most-common-spring-framework-mistakes
- https://spring.io/blog/2015/11/29/how-not-to-hate-spring-in-2016
- https://www.quora.com/Why-do-most-programmers-whose-primary-language-is-not-Java-seem-to-have-unfavorable-opinions-of-the-Spring-Framework-and-what-do-they-dislike-about-its-philosophy
- https://samatkinson.com/why-i-hate-spring/
- https://blog.jakubholy.net/2020/spring-nevermore/
- https://youtu.be/CT8dbbe783s

## Mistakes 

