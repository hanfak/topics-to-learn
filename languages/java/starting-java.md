# Starting java

Take this from a Java developer working for multinational company creating middleware enterprise applications with lots of integration between internal and external services.

Depends on what you want to do. If learning java, then it is quite simple, do the aiport challenge and other tasks (ie fizzbuzz) that your did at makers in Java:

For doing the airport/fizzbuzz exercise:

I would use pure vanilla java, and avoid using libraries (apart from the java supplied one) and annotations for production code.

I would implement a main method, although this is not necessary, but will help you hava an app which you can run from the command line.

Language: Java 8 or 11 (long term support versions). Majority of software is still written in java8
Testing: Junit 4 (version 5 is new and different so not as widely supported)
Testing libraries: AssertJ to write cleaner and fluent tests (Hamcrest is popular but has lots issues)
Mocking: Mockito
IDE: Intellij - This makes things very simple, I would first learn how to compile and run your code using the terminal. Learn how to use the debug features in your IDE!! Intellij is the best IDE
Build and dependency management: Maven or Gradle - You want to be  able to use the build to run your tests and build your jar (avoid Ant, I have had to deal with it and it is not pretty). For maven, look at maven-assembly-plugin for building jar
Patterns: All the stuff you learned at makers (ie SOLID)

For more complex projects, ie building a webservice (crud app):

Build a crud (needs a database) app that talks to 3rd party services (ie weather app), does some logic with inputs and services, and return something.

This will mean using different libraries. I would suggest doing two versions, one using pure libraries, the other using frameworks (ie spring, hibernate).

When I talk about logic, I mean doing some sort of decision (ie predicate, if) based on some rules. We do this with data, ie:

- inputs to app (ie http request, jms message, command line input)
- data in persistence (ie files, database)
- Getting more data outside of app (ie external http response)

Types of rules, ie:

- If the weather is stormy, then no planes can land or take off
- If the value1 is less than 5 and value 2 equals 10 then (if value 3 greater than 9 then return true else return false) else return false

For lots of rules on different data, we use **rules engines**

There is also workflows, which dictate how a business journey for a usecase should occur. The type of workflow depends not only on business logic, but also on non functional requirements of the system and technology available.

Pure version:

there is a lot here, so might feel a lot to learn, but doing stuff like this will help you learn the language and design, and how this works compared to using a framework.

All the above plus
Libraries:
  - jetty - embedded webserver to allow for connections via the web. This also means using servlets. (Can use Tomcat, but this is not an embedded server, not greate for containerising your application) see https://codeforfunandmoney.wordpress.com/2016/07/20/embedded-jetty-server-example/
  - Apache Http client - This will allow you to connect to a 3rd party services (Java 11 has its own, but not very mature. apache has a standard one). Another one is unirest.
  - apache commons lang3 - to help override hashcode() and equals() methods for types. Can let your IDE create it for you. Remember to test
  - SLF4J - This will help with creating logs
  - Logbook by zalando - logging incoming and outgoing calls to the app
  - Hikari or c3po - To create database connections, using object pooling pattern to improve performance when using a database
  - Jdbc - allow you to communicate with the database, this does mean using sql. Need specific ones for your type of db
  - flywaydb - to perform sql migration, ie setup your database, tables etc with out having to run it via the terminal
  - yatsepc - acceptance testing framework, very popular at my work (see https://codeforfunandmoney.wordpress.com/ for examples on how to use and the repo https://github.com/bodar/yatspec). Other common ones are cucumber, concordion
  - Other libraries depending on what logics you are performing like guava, math etc
Patterns:
  - Use of Clean/hexagonal architecture, which means using SOLID principles to organise classes and calls etc, to make your code more maintainable and extendable. (see https://github.com/mattia-battiston/clean-architecture-example uses spring but should be easy to follow)
  - Object pooling, to help create expensive objects (ie database connections) at the startof the application, instead when needed, and just use them when necessary.
  - Use of properties, create property files in resource directory, and have different ones for different environments (ie prod and test). So for example using different endpoints for differnt db you will use in test and prod environments
  - Functional programming - use of lambdas,streams, optional, immutable objects, should be standard through out your code
  - Wiring - This is where you build all your objects (new them up) and is called when you run the main method (start the app up). Known as service locator pattern or factories
  - Design patterns - Builder, factory, static factory methods, strategy, domain objects, repository, facade, adapter (https://github.com/iluwatar/java-design-patterns for examples)
  - return Json or xml, build these up yourself instead of using a framework like jackson
DevOps:
  - Docker: To containerise your app, to be able to run anywhere where docker is installed
  - Kubernetes: This is much more than you need, this is to help manage your containers, number of replicas, etc
  - Deploy to aws or google cloud


Have a look at my project, it is not all uniform code as i was exploring diferent ways of doing stuff, but follows and uses the above https://github.com/hanfak/ShopOfHan/

Framework version:

Using frameworks means you are beholden to the framework as you write code for it (just like rails). where as libraries your code uses it when it needs it (dont need it to run your app). A lot of frameworks use annotations and reflection, which makes it hard to debug when your need to investigate, there is a lot of magic, makes it hard to see how things connect. Also frameworks can make it difficult if you want to do something which is not what they expect or improve performance. But frameworks makes it easy to build and create from scratch and a build at a faster speed. I would suggest using https://github.com/mattia-battiston/clean-architecture-example as way of not having your app totally beholden a framework, by using clean architecture.

- Will need to use some of the above libraries and patterns here to0
- Use Spring - Spring boot (for wiring, new up objects), spring web (for creating webservice) see https://spring.io/guides
- Use hibernate (an ORM like datamapper) to interact with db wihtout using sql (also spring data and jdbc template which comes with spring). Not a fan of this, especially when it comes to complex sql queries.
- Jackson - to help create create json from objects and vice versa
- lombok - removes a lot of boiler plate. I am not real fan using annotations in code, as they use 'reflection', and thus makes it hard to debug

Other things to use or learn:

- Use a stub, like wiremock, to stub a 3rd party service over http so that a dummy one is used but you control the response. (http://wiremock.org/ ). Useful for automated end to end tests
- Use of multi threading (complex so would not bother for now, but should learn this especially for apps that deals with lots of requests)
- completable futures for aysnc programming
- messaging queues like activemq or rabbitmq
- file transfers
- event sourcing, cqrs, aggreagates (domain driven design)
- Use your build ie maven, to run static analysis ie findbugs, pmd, pitest, jacoco. To help improve standards, coverage etc
- Use jenkins or travis to run builds whenever you make a push to your repo
- create a status page which is accesed on a end point, and gives the health of the app (are all dependencies up ie is the database up, is a 3rd party uri up)
- display metrics from an end point, jvm memory etc
- Allow your app to handle https, inclduing certificates
- Make sure app doesnot break (ie throw exceptions which crashes the program)
- Use a scheduler, which runs a cron job to hit an end point to do something. Common library is Quartz
