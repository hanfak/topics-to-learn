# Why use java

- widely used
- older systems written in java
- backwards compatibility, stable platform
- support from owner and community
- Mature libraries and frameworks, and lots of them
- write once run anywhere
- efficient memory management, Automatic Garbage Collection
- Easy to hire, comp sci grads learn java
- Highly scalable, good support for concurrency, multithreading
- Good testing libraries
- Good support for integration (servlets/http, message brokers)
- Good integration with databases
- platform independent
- No licensing costs (if on non oracle)
- statically typed, compiler spots problems first
- Great IDEs
- Good build tools (maven)
- JVM, tooling (jconsole, Java Flight Recorder and Mission Control), jmx for dynamic management of app
- jvm separate from language, can have multiple languages running on it
- Increased number of languages on jvm, and some of these can use java libraries and frameworks, as well as tooling
- Easy to learn
- Better secruity
- Standards - https://docs.oracle.com/javase/specs/
- high performance, internal jvm performance always improving

## links

- https://www.devteam.space/blog/why-should-you-use-java-for-your-backend-infrastructure/
- https://medium.com/webbasedevelopment/why-java-is-the-most-preferred-programming-language-for-building-end-to-end-enterprise-solutions-731027246f2a
- https://www.invensis.net/blog/it/benefits-of-java-over-other-programming-languages/
- https://developer.okta.com/blog/2019/07/15/java-myths-2019
- https://medium.com/hackernoon/the-good-and-the-bad-of-java-programming-eeaee8918ea
- https://blog.jetbrains.com/idea/2020/05/25-things-we-love-about-java/

## Downsides

- deployables are larger
  - This means all dependencies have to be included for deployment, whether rolled into a single JAR or across various components (WAR file + app server + JRE + dependencies). This affects the size of the deployment.
- the syntax is verbose
  - It was created at the time using C syntax
    - but now java 8+ can use functional style
  - Lack of dynamic typing
    - Some see as good, some as bad. For massive projects worked on by many people static typing is good
    - Static typing and verbosity tells the developer what is happening
- Due to backwards compatibility, this can lead to non efficient changes being made
  - As old ways are still there, developers can still use them, when it is better to use better ways
- Lack of control of memory
  - This is still possible, but not advised
  - Best use C if you want this
