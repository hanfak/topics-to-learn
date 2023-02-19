# Annotations

## Custom Annotations

- https://www.baeldung.com/java-custom-annotation
- https://mkyong.com/java/java-custom-annotations-example/
- https://www.javatpoint.com/java-annotation
- https://youtu.be/DkZr7_c9ry8 coding with john: Annotations In Java Tutorial - How To Create And Use Your Own Custom Annotations

## Links

- https://dzone.com/articles/creating-custom-annotations-in-java
- https://dzone.com/videos/devnexus2015/how-annotations-work-java?utm_medium=feed&utm_source=feedpress.me&utm_campaign=Feed:%20dzone%2Fjava

## why

- Allows for usage of frameworks
-  save plenty of time by configuring everything in our application using annotations.
- Reduce amount of code written (verbosity)
- Can abstracts (specially for less experienced developers) some of the common issues we normally have to deal with when building software.
  - Avoid problems
- to achieve some consistency across teams.
- Better than having configuration in an xml
- speed of writing code, starting up
- https://stackoverflow.com/questions/4285592/why-java-annotations


## The bad

- https://www.yegor256.com/2016/04/12/java-annotations-are-evil.html

  - there is one big problem with annotations—they encourage us to implement object functionality outside of an object, which is against the very principle of encapsulation.
  - The control is lost (not inverted, but lost!). The object is not in charge any more. It can’t be responsible for what’s happening to it.
  - That’s because we don’t want to duplicate the same code over and over again, right? That’s correct, duplication is bad, but tearing an object apart is even worse.
  - Object composition, which is the most important process in object design, is hidden somewhere behind the scenes.... We must see how our objects are composed. We may not care about how they work, but we must see the entire composition process.
  - Code pollution
    - Can have multiple annotations, inline annotations
  - Not Comprehensible
    - Annotations are just meta data and the actual effect happens somewhere else in a framework or an annotation processor
    - It is not (always) possible to navigate to the code that performs the logic linked to the annotation.
    -  forces us to be jumping from one place to the other and do searches in our codebase to try to understand where everything is being configured.
  - May fail silently
    - At runtime
  - Difficult to extend
    - writing a custom annotation is relative simple, the logic for annotation processing and integration into a framework might be complicated.
    - fight against the framework, if you dont want to do the things the way it is made for
  - Limited Compiler Support
    - annotations are a language in a language without good compiler support.
  - Reliance on reflection
  - Magic
      -  it’s impossible to understand or even follow the code if you’re not familiar with both the framework and the codebase!
      - Can be harder to get devs to learn, esp with custom annotations
  - Overreliance on the annotation
    - ie framework developers
    - Not understanding the cost, and possible simpler/lightweight/clearer solutions
    - dont understand how it works
  - Possibly Introducing New Weaknesses (for frameworks)
    - pull in extra dependencies, more chance of security issues and vulnerabilities
  - Performance implications
    - especially without understanding it
    - ie mockito annotation add a lot of overhead to running tess with it's annotations, this reduces dev productivity and increase costs
  - Debugging becomes difficult
    - Not easy to find where the problem is through the flow of the code (stack trace, debugger)
    - Unless very experienced with issues, end up researching solutions

- https://blog.softwaremill.com/the-case-against-annotations-4b2fb170ed67
- https://javadevguy.wordpress.com/2016/01/13/evil-annotations/
- https://dzone.com/articles/are-annotations-bad
- https://doanduyhai.wordpress.com/2012/04/21/magics-is-evil/
- https://blog.softwaremill.com/the-case-against-annotations-4b2fb170ed67
- https://www.quora.com/How-are-Java-Annotations-a-good-thing-Dont-they-mess-up-the-understandability-of-whats-really-going-on-in-the-code/answer/Alan-Mellor?ch=15&oid=266552112&share=005a2c81&srid=3c80F&target_type=answer
- https://theboreddev.com/the-problems-of-annotation-driven-development/
