


## Why bad

- https://www.yegor256.com/2014/10/03/di-containers-are-evil.html
- https://www.tonymarston.net/php-mysql/dependency-injection-is-evil.html
- http://davidscode.com/blog/2015/04/17/when-does-dependency-injection-become-an-anti-pattern/
- https://www.continuousimprover.com/2018/05/dont-blame-dependency-injection.html


### notes

Dependency Injection Makes Code Unintelligible

Dependency Injection (DI) has become pervasive due to frameworks such as Spring and J2EE and libraries such as Guice. DI's aim is to make configuration and mapping of objects easier and reduce (or eliminate) coupling between services and implementations. These are good goals. Coupling of objects can lead to brittle and hard to maintain code. Configuration and linking of services to implementations can be tedious and error prone. Does DI accomplish these goals?

Coupling
DI removes coupling completely from the code. The relationship between interface and implementation is coded in external files or meta-data. In the case of Spring (up until recently) the relationships are specified in cumbersome XML files. Guice (and now Spring) specify the relationships with annotations. If too much coupling is bad does it imply that no coupling is good? No. We need some coupling so that we can understand how classes relate to one another. Maintainers of a code base need to be able to discover how various classes relate to one another and be able to trace class usage and interdependence. Hiding all of this complexity in XML files and annotations leaves the application impenetrable.

Configuration
DI presents a shell game in terms of configuration. The programmer can change behavior without changing any lines of code. But wait - XML _is_ code. Annotations _are_ code. There is no benefit to moving a specification from a Java file into an XML file. In fact, it's worse as you've moved from a well understood, well supported syntax into a horrible syntax (see my earlier post on XML).

Unit Tests?
DI has gained support from the Test Driven Development community as it makes running tests easier. TDD is a bad idea (see my earlier post). Adding DI to the mix makes it worse.

Bad Nomenclature
The term "Dependency Injection" is horrible. When I first heard it I had no idea what it meant. Inversion of Control was a much better term; at least it suggests what it does. Tangentially, we are being inundated with new terms and acronyms that are unnecessary and confusing (the AOP world is one of the worst offenders).

What's Wrong with Plain Ol Java?
DI is part of a trend of methodologies that appear to hate the Java language. We keep seeing frameworks and libraries that turn XML and annotations into domain specific languages. There's a kind of sexiness to this. Watching Guice auto-magically connect up lots of objects is cool but I want to get my job done not be cool.

Which would you rather see?
Imagine you've just been hired to take over a very large (1 million line plus) code base. Which would you rather see?

```
 myObj.setImplementation(new myImplementation());
```

or

```
 @Inject
 public class myInt
 {
  public(@Named("config.me")String s);
 }
```
or

 100 lines of XML


I'll take the good 'ol simple 1 line of Java every time.
