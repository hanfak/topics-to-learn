Opinionated guide


<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Not Your Father's Java: An Opinionated Guide to Modern Java Development, Part 1](#not-your-fathers-java-an-opinionated-guide-to-modern-java-development-part-1)
- [The JVM](#the-jvm)
- [The Build](#the-build)
	- [Gradle init directory structure](#gradle-init-directory-structure)
- [The IDE](#the-ide)
- [Documenting Your Code in Markdown](#documenting-your-code-in-markdown)
- [Write Succinct Code with Java 8](#write-succinct-code-with-java-8)
- [Simple Lightweight Concurrency with Fibers](#simple-lightweight-concurrency-with-fibers)
- [Fault-Tolerant Actors and Hot Code Swapping](#fault-tolerant-actors-and-hot-code-swapping)
- [Advanced Topic: Pluggable Types](#advanced-topic-pluggable-types)
- [Wrapping Up (For Now)](#wrapping-up-for-now)
- [An Opinionated Guide to Modern Java, Part 2: Deployment, Monitoring & Management, Profiling and Benchmarking](#an-opinionated-guide-to-modern-java-part-2-deployment-monitoring-management-profiling-and-benchmarking)
- [Preamble](#preamble)
- [Modern Java Packaging and Deployment](#modern-java-packaging-and-deployment)
- [Capsule](#capsule)
- [Logging](#logging)
- [Monitoring and Management with jcmd and jstat](#monitoring-and-management-with-jcmd-and-jstat)
- [Monitoring and Management with JMX](#monitoring-and-management-with-jmx)
	- [Jolokia](#jolokia)
- [Easy Health and Performance Monitoring with Metrics](#easy-health-and-performance-monitoring-with-metrics)
- [Profiling](#profiling)
- [Advanced Topic: Profiling and Debugging with Byteman](#advanced-topic-profiling-and-debugging-with-byteman)
- [Advanced Topic: Benchmarking with JMH](#advanced-topic-benchmarking-with-jmh)
- [So, What Have We Learned So Far?](#so-what-have-we-learned-so-far)
- [An Opinionated Guide to Modern Java, Part 3: Web Development](#an-opinionated-guide-to-modern-java-part-3-web-development)
- [Preamble](#preamble)
- [Introduction to Modern Java Web Development](#introduction-to-modern-java-web-development)
- [HTTP Services with JAX-RS and Dropwizard](#http-services-with-jax-rs-and-dropwizard)
- [Dropwizrd](#dropwizrd)
- [HTTP Clients](#http-clients)
- [Database Access](#database-access)
	- [JDBI](#jdbi)
	- [JOOQ](#jooq)
- [Dependency Injection](#dependency-injection)
	- [Dagger](#dagger)
- [Advanced Topic: Blocking vs. Non-blocking or Synchronous vs. Asynchronous](#advanced-topic-blocking-vs-non-blocking-or-synchronous-vs-asynchronous)
- [Advanced Topic: Interactive Web Services with Web Actors](#advanced-topic-interactive-web-services-with-web-actors)

<!-- /TOC -->


# Not Your Father's Java: An Opinionated Guide to Modern Java Development, Part 1

More working, useful code has been written in the Java programming language than in any other in history, with the possible exceptions of C and COBOL. When Java was released almost 20 years ago, it took the software world by storm. It was **a simpler, safer, alternative to C++, and some time later its performance caught up, too** (depending on the exact usage, a large Java program can be slightly slower, as fast, or a little faster than a comparable C++ codebase). It offered truly tremendous productivity benefits over C++, while sacrificing very little (if anything at all) in return.

Java is a blue-collar language – the working person’s trusty tool – **adopting only tried and true idioms, and adding features only if they solve major pain points**. Whether or not Java has stayed true to its mission or not is an open question, but it certainly tries not to let current fashions sway it too far off course. Java has been used to write code for anything from smart-cards, through embedded devices, and all the way to mainframes. It is even being used to write mission- and safety-critical hard realtime software.

And yet, in recent years, the Java programming language has gained some noteriety as well, especially among web startups. **Java is verbose** relative to languages like Ruby or Python, and its web frameworks used to require extensive amounts of XML configuration, especially when compared to configuration-free frameworks like Rails. In addition, Java’s widespread use in large enterprise companies led to the adoption of programming patterns and practices that might have a place in a very large programming team working for a company with extensive bureaucracy, but do not belong in a fast-moving-things-breaking startup.

But all the while, Java has changed. The language recently acquired lambda expression and traits; libraries provide it with true lightweight threads – just like Erlang’s and Go’s. And, most importantly, a more modern, lightweight approach now guides API, library and framework design, replacing all the old heavyweight, XML-laden ones.

Another thing has happened in the Java ecosystem in the past few years: a bunch of good implementations of alternative languages for the JVM have started gaining popularity; some of those languages are quite good (my personal favorites are Clojure and Kotlin). But even with those languages as viable (and sometimes recommended) options, Java does have several advantage over other JVM languages, among them: **familiarity, support, maturity, and community.** With modern tools and modern libraries, Java actually has a lot going for it. It is not surprising, thenrefore, that many Silicon Valley startups, once they grow a bit, come back to Java, or, at the very least – to the JVM.

This opinionated, introductory guide is intended for the Java programmer (all 9 million of them) who wants to learn how to write modern, lean Java, or for the Python/Ruby/Javascript programmer who’s heard (or may have experienced) bad things about Java and is curious to see how things have changed and how they can get Java’s awesome performance, flexibility and monitoring without sacrificing too much coolness.

# The JVM

- For those unfamiliar with Java terminology, Java is conceptually made of three parts: Java, the programming language, the Java runtime libraries, and the Java Virtual Machine, or JVM.
  - If you’re familiar with Node.js, Java the language is analogous to JavaScript, the runtime libraries are analogous to Node.js itself, and the JVM would be analogous to V8.

- The JVM and runtime libraries are packaged together into what is known as the Java Runtime Environment, or the JRE (although often when people say “JVM” they actually mean the entire JRE).
- The Java Development Kit, or the JDK, is a version of the JRE that includes development tools like javac, the Java compiler, and various monitoring and profiling tools.
- The JRE comes in several flavors, like those made for embedded devices, but in this blog post series, we will only be referring to the JRE made for server (or desktop) machines, known as Java SE (Standard Edition).

- there are quite a few implementations of the JVM (or the JRE) – some are open-source and some are commercial.
  - Some are highly specific: for example, there are JVMs for hard-realtime embedded software, and those made for huge RAM sizes (in the hundreds of gigabytes).
  - But we will be using HotSpot, the free, “common” JVM implementation made by Oracle, which is also available as part of the open-source OpenJDK.

- Java was built for the JVM, and the JVM was built for Java (recently, though, the JVM has undergone some modifications specifically with other programming languages in mind).
- But what is the JVM?
  - the JVM is an abstraction-implementation magic machine.
  - It takes nice, simple, and useful abstractions, like infinite memory and polymorphism – which sound costly to implement – and implements them so efficiently that they can easily compete with runtimes that don’t provide these useful abstractions.
  - More specifically, the JVM has the best garbage collection implementations in widespread production use,
  - and its JIT allows it to inline and optimize virtual method calls (which are at the core of the most useful abstractions in most programming languages), making them extremely cheap while preserving all of their usefulness.
  - The JVM’s JIT (Just-In-Time compiler) is basically a highly advanced profile guided optimizing compiler running concurrently with your application.
- The JVM also hides many of the idiosyncracies of the underlying hardware/OS platform,
  - like the memory model (how and when code running on different CPU cores sees changes to variables made on other cores) and access to timers.
  -  It also offers dynamic runtime-linking of all code, hot code swapping, and monitoring of pretty much everything that’s going on in the JVM itself, and in the Java libraries.
- That is not to say that the JVM is perfect.
  - Right now its missing the possibility to embed complex structs inside arrays (this is scheduled to be resolved in Java 9), and proper tail-call optimization.
  - Nevertheless, **the JVM is so mature, well-tested, fast, flexible, and allows for such detailed runtime profiling and monitoring**, that I wouldn’t consider running a critical, non-trivial server process on anything else.


# The Build

- Java has had several build tools over its longish history (Ant, Maven), and yes, most of them were based on XML.
  - But the modern Java developer uses Gradle (which has recently become Android’s official build tool).
  - Gradle is a mature, heavily developed, modern Java build tool, that uses a DSL built on top of the Groovy language to specify the build process.
  - It combines the simplicity of Maven with the power and flexibility of Ant, while throwing away all that XML.
  - But Gradle is not without its faults: while it makes the most common things easy and declaratives, there are quite a few things that are quite, though not very, common, but still require dropping down to imperative Groovy.

## Gradle init directory structure

- Our source code goes into src/main/java/ while our test code goes in src/test/java/.

- Now, we’ll modify build.gradle in the main project directory to be:

```java
apply plugin: 'java'
apply plugin: 'application'

sourceCompatibility = '1.8'

mainClassName = 'jmodern.Main'

repositories {
    mavenCentral()
}

dependencies {
    compile 'com.google.guava:guava:17.0'

    testCompile 'junit:junit:4.11' // A dependency for a test framework.
}

run {
    systemProperty 'jmodern.name', 'Jack'
}
```
- The build file sets jmodern.Main as the main class, it declares Guava as a dependency, and sets the value of the jmodern.name system property, which we read in our program.

- When we run: `gradle run`
  - Gradle will download Guava from Maven Central, compile our program, and run it with Guava on the classpath, and jmodern.name set to "Jack". That’s it.

- To run the unit tests: `gradle build`
  - The test report, now found in build/reports/tests/index.html, looks like this: `Gradle test report`

# The IDE

- Some people say that IDEs are there to hide problems with the programming language. Well, I don’t have an opinion about that, but having a good IDE always helps, regardless of the programming language you’re using, and Java’s got the best around.
-  While the choice of an IDE is not as important as anything else in this article, of the “big three” Java IDEs: Eclipse, IntelliJ IDEA, and NetBeans, you should really use either IntelliJ or NetBeans.
- IntelliJ is probably the most powerful of the three, while NetBeans is the most intuitive and easiest to get started with (and, in my opinion, the best looking). Also, NetBeans has the best Gradle support thanks to the Gradle plugin (which can be installed by going to Tools -> Plugins -> Available Plugins). Eclipse is (still?) the most popular of the three. I abandoned it some years ago, and from what I hear it’s become kind of a mess, but if you’re a long-time Eclipse user and are happy with it, that’s OK, too.

# Documenting Your Code in Markdown

- Java has long had really good API documentation with **Javadoc**, and Java developers are accustomed to writing Javadoc comments.
- But the modern Java developer likes **Markdown**, and would like to write spice up their Javadoc with Markdown.
- To do that, we will use the Pegdown Doclet project (a Doclet is a Javadoc plugin) by making the following additions to our build file: Before the dependencies section, we will add
```
configurations {
    markdownDoclet
}
```

and we’ll add this line to dependencies:
```
markdownDoclet 'ch.raffael.pegdown-doclet:pegdown-doclet:1.1.1'
```

Finally, put this somewhere in the build file:

```
javadoc.options {
    docletpath = configurations.markdownDoclet.files.asType(List) // gradle should relly make this simpler
    doclet = "ch.raffael.doclets.pegdown.PegdownDoclet"
    addStringOption("parse-timeout", "10")
}
```

- For mavne alternative: https://www.mscharhag.com/java/using-markdown-syntax-in-javadoc

- To test our setup, let’s add a fancy Markdown Javadoc to a method called randomString (which we’ll write in the next section):

```java
/**
 * ## The Random String Generator
 *
 * This method doesn't do much, except for generating a random string. It:
 *
 *  * Generates a random string at a given length, `length`
 *  * Uses only characters in the range given by `from` and `to`.
 *
 * Example:
 *
 * ```java
 * randomString(new Random(), 'a', 'z', 10);
 * ```
 *
 * @param r      the random number generator
 * @param from   the first character in the character range, inclusive
 * @param to     the last character in the character range, inclusive
 * @param length the length of the generated string
 * @return the generated string of length `length`
 */
public static String randomString(Random r, char from, char to, int length) ...

```

- Then, generate the javadocs with ~, which will put the html files in build/docs/javadoc/.

- I don’t use markdown in comments often, as they don’t render well in IDEs. But this does make life much easier when you want to include code examples in your Javadoc.

# Write Succinct Code with Java 8

- The recent release of Java brought the biggest change to the language since its original release with the addition of lambda expressions.
- Lambda expressions (with type inference) address one of the biggest issues people have had with the Java language, namely unjustified verbosity when doing simple stuff.
- To see how much lambda expressions help, I took the most infuriatingly verbose, simple data manipulation example I could think of, and wrote it in Java 8.
  - It generates a list of random “student names” (just random strings), groups them by their first letter, and prints out a nicely formatted student directory. So now let’s run our program after changing our Main class to this:

```java
package jmodern;

import java.util.List;
import java.util.Map;
import java.util.Random;
import static java.util.stream.Collectors.*;
import static java.util.stream.IntStream.range;

public class Main {
    public static void main(String[] args) {
        // generate a list of 100 random names
        List<String> students = range(0, 100).mapToObj(i -> randomString(new Random(), 'A', 'Z', 10)).collect(toList());

        // sort names and group by the first letter
        Map<Character, List<String>> directory = students.stream().sorted().collect(groupingBy(name -> name.charAt(0)));

        // print a nicely-formatted student directory
        directory.forEach((letter, names) -> System.out.println(letter + "\n\t" + names.stream().collect(joining("\n\t"))));
    }

    public static String randomString(Random r, char from, char to, int length) {
        return r.ints(from, to + 1).limit(length).mapToObj(x -> Character.toString((char)x)).collect(joining());
    }
}
```

- Java infers the types of all lambdas’ arguments, but everything is still type safe, and if you’re using an IDE, you’ll get autocomplete and refactoring for all type-inferred variables.
- Java does not infer types for local variables (like the auto keyword in C++ or var in C# or Go) because that would arguably hurt code readability.
- But that doesn’t mean you have to manually type the types (heh).
- For example, type Alt+Enter in NetBeans on this line: `students.stream().sorted().collect(Collectors.groupingBy(name -> name.charAt(0)))` and the IDE will assign the result to a local variable of the appropriate type (in this case, Map<Character, String>).

- If we wanted to go a little crazier with the functional style, we could write the main method like so:

```java
public static void main(String[] args) {
    range(0, 100)
            .mapToObj(i -> randomString(new Random(), 'A', 'Z', 10))
            .sorted()
            .collect(groupingBy(name -> name.charAt(0)))
            .forEach((letter, names) -> System.out.println(letter + "\n\t" + names.stream().collect(joining("\n\t"))));
}
```

- Not your father’s Java, indeed (look ma, no types!), but I would say that taking this too far would certainly go against the spirit of the language.

- Even though Java has lambdas, it doesn’t have function types.
  - Instead, lambda expressions are eventually converted to an appropriate functional interface, namely an interface with a single abstract method.
  - This automatically makes a lot of legacy code work beautifully with lambdas.
  - For example,
    - the `Arrays.sort` method has always taken an instance of the Comparator interface, which simply specifies the single abstract int compare(T o1, T o2) method.
    - In Java 8, a lambda expression can be used to sort an array of strings according to their third character: `Arrays.sort(array, (a, b) -> a.charAt(2) - b.charAt(2));`
- Java 8 also added the ability to include method implementations in interfaces (which turns them into what is known as “traits”).
- For example, the FooBar interface below contains two methods, one abstract (foo) and the other (bar) with a default implementation. The useFooBar method, well, uses a FooBar:

```java
interface FooBar {
    int foo(int x);
    default boolean bar(int x) { return true; }
}

int useFooBar(int x, FooBar fb) {
    return fb.bar(x) ? fb.foo(x) : -1;
}
```

- Even though FooBar has two methods, only one of them (foo) is abstract, so it is still a functional interface, and can be created with a lambda expression. For example, the call: `useFooBar(3, x -> x * x)` will return 9.

# Simple Lightweight Concurrency with Fibers

- For people like me, who are interested in concurrent data structures, the JVM is paradise.
- On the one hand, it gives you low-level access to the CPU’s concurrency primitives like CAS instructions and memory fences, while on the other it gives you a platform-neutral memory model combined with world-class garbage collectors;
- the combination is everything you want when building high-performance concurrent data structures. But for those who **use concurrency not because they want to but becuase they have to in order to scale their software – namely, everyone else** – the Java’s concurrency story is problematic.
- True, Java was designed for concurrency from the get-go, and places a lot of emphasis on its concurrency constructs in every release.
- It’s got state-of-the-art implementations of very useful concurrent data structures (like ConcurrentHashMap, ConcurrentSkipListMap, and ConcurrentLinkedQueue) – not even Erlang and Go have those – and is usually 5 years or more ahead of C++ when it comes to concurrency, but using all this stuff correctly and efficiently is pretty damn hard.
- First we had threads and locks, and those worked fine for a while, until we needed more concurrency and that approach didn’t scale very well.
- Then we had thread pools and events: those scale quite well, but can even be harder to reason about, especially in a language that does not protect against racy mutation of shared state.
- Besides, if your problem is that kernel threads don’t scale well, then asynchronous handling of events is a bad idea.
- Why not simply fix threads?
  - That’s precisely the approach taken by Erlang and (much later) Go: lightweight, user-mode threads. Those allow mapping domain concurrency (like number of concurrent users) directly to program concurrency (lightweight threads). They allow for a simple, familiar, blocking programming style without sacrificing scalability, and for efficient use of synchronization constructs simpler than locks and semaphores.

- Quasar is an open-source library made by us, that adds true lightweight threads to the JVM (in Quasar they’re called fibers), where they can work naturally alongside plain (OS) threads. Quasar also has CSP mechanisms just like Go’s, and a very Erlang-like actor system. Fibers are certainly the modern developer’s weapon of choice when it comes to concurrency. They are simple, elegant and very performant. Let’s play with them for a bit.

First, we’ll setup the build. Merge the following into build.gradle:

configurations {
    quasar
}

dependencies {
    compile "co.paralleluniverse:quasar-core:0.5.0:jdk8"
    quasar "co.paralleluniverse:quasar-core:0.5.0:jdk8"
}

run {
    jvmArgs "-javaagent:${configurations.quasar.iterator().next()}" // gradle should make this simpler, too
}
This will be our new Main.java (if you’re using NetBeans, you’ll want to right-click the project and select “Reload Project” after adding the new dependencies):

package jmodern;

import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.strands.Strand;
import co.paralleluniverse.strands.channels.Channel;
import co.paralleluniverse.strands.channels.Channels;

public class Main {
    public static void main(String[] args) throws Exception {
        final Channel<Integer> ch = Channels.newChannel(0);

        new Fiber<Void>(() -> {
            for (int i = 0; i < 10; i++) {
                Strand.sleep(100);
                ch.send(i);
            }
            ch.close();
        }).start();

        new Fiber<Void>(() -> {
            Integer x;
            while((x = ch.receive()) != null)
                System.out.println("--> " + x);
        }).start().join(); // join waits for this fiber to finish
    }
}
We now have two fibers communicating via a channel.

Strand.sleep, and all of the Strand class’s methods, work equally well whether we run our code in a fiber or a plain Java thread. Let’s now replace the first fiber with a plain (heavyweight) thread:

new Thread(Strand.toRunnable(() -> {
    for (int i = 0; i < 10; i++) {
        Strand.sleep(100);
        ch.send(i);
    }
    ch.close();
})).start();
and this works just as well (of course, we could have millions of fibers running in our app, but only up to a few thousand threads).

Now, let’s try channel selection (which mimics Go’s select statement):

package jmodern;

import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.strands.Strand;
import co.paralleluniverse.strands.channels.Channel;
import co.paralleluniverse.strands.channels.Channels;
import co.paralleluniverse.strands.channels.SelectAction;
import static co.paralleluniverse.strands.channels.Selector.*;

public class Main {
    public static void main(String[] args) throws Exception {
        final Channel<Integer> ch1 = Channels.newChannel(0);
        final Channel<String> ch2 = Channels.newChannel(0);

        new Fiber<Void>(() -> {
            for (int i = 0; i < 10; i++) {
                Strand.sleep(100);
                ch1.send(i);
            }
            ch1.close();
        }).start();

        new Fiber<Void>(() -> {
            for (int i = 0; i < 10; i++) {
                Strand.sleep(130);
                ch2.send(Character.toString((char)('a' + i)));
            }
            ch2.close();
        }).start();

        new Fiber<Void>(() -> {
            for (int i = 0; i < 10; i++) {
                SelectAction<Object> sa
                        = select(receive(ch1),
                                receive(ch2));
                switch (sa.index()) {
                    case 0:
                        System.out.println(sa.message() != null ? "Got a number: " + (int) sa.message() : "ch1 closed");
                        break;
                    case 1:
                        System.out.println(sa.message() != null ? "Got a string: " + (String) sa.message() : "ch2 closed");
                        break;
                }
            }
        }).start().join(); // join waits for this fiber to finish
    }
}
Starting with Quasar 0.6.0 (in development), you can use lambda expressions directly in the select statement (to try this at home, you’ll need to change Quasar’s version in the build file from 0.5.0 to 0.6.0-SNAPSHOT and add maven { url "https://oss.sonatype.org/content/repositories/snapshots" } to the repositories section), so the code running in the last fiber could also be written so:

for (int i = 0; i < 10; i++) {
    select(
        receive(ch1, x -> System.out.println(x != null ? "Got a number: " + x : "ch1 closed")),
        receive(ch2, x -> System.out.println(x != null ? "Got a string: " + x : "ch2 closed")));
}
Now let’s try some high-performance IO with fibers:

package jmodern;

import co.paralleluniverse.fibers.*;
import co.paralleluniverse.fibers.io.*;
import java.io.IOException;
import java.net.InetSocketAddress;
import java.nio.*;
import java.nio.charset.*;

public class Main {
    static final int PORT = 1234;
    static final Charset charset = Charset.forName("UTF-8");

    public static void main(String[] args) throws Exception {
        new Fiber(() -> {
            try {
                System.out.println("Starting server");
                FiberServerSocketChannel socket = FiberServerSocketChannel.open().bind(new InetSocketAddress(PORT));
                for (;;) {
                    FiberSocketChannel ch = socket.accept();
                    new Fiber(() -> {
                        try {
                            ByteBuffer buf = ByteBuffer.allocateDirect(1024);
                            int n = ch.read(buf);
                            String response = "HTTP/1.0 200 OK\r\nDate: Fri, 31 Dec 1999 23:59:59 GMT\r\n"
                                            + "Content-Type: text/html\r\nContent-Length: 0\r\n\r\n";
                            n = ch.write(charset.newEncoder().encode(CharBuffer.wrap(response)));
                            ch.close();
                        } catch (IOException e) {
                            e.printStackTrace();
                        }
                    }).start();
                }
            } catch (IOException e) {
                e.printStackTrace();
            }
        }).start();
        System.out.println("started");
        Thread.sleep(Long.MAX_VALUE);
    }
}
What have we done here? First, w**e launch a fiber that will loop forever, accepting TCP connection attempts. For each accepted connection, it spawns another fiber that reads the request, sends a response and then terminates.** While this code is blocking on IO calls, under the covers it uses async EPoll-based IO, so it will scale as well as any async IO server (we’ve greatly improved IO performance in Quasar 0.6.0-SNAPSHOT).

# Fault-Tolerant Actors and Hot Code Swapping

- The actor model, (semi-)popularized by the Erlang language, is intended for the writing of fault-tolerant, highly maintainable applications.
- It breaks the application into independent fault-containment units – actors – and formalizes the handling of and recovery from errors.

Before we start playing with actors, we’ll need to add this dependency to the dependencies section in the build file: compile "co.paralleluniverse:quasar-actors:0.5.0".

Now let’s rewrite our Main class yet again, this time the code is more complicated as we want our app to be fault tolerant:

package jmodern;

import co.paralleluniverse.actors.*;
import co.paralleluniverse.fibers.*;
import co.paralleluniverse.strands.Strand;
import java.util.Objects;
import java.util.concurrent.ThreadLocalRandom;
import java.util.concurrent.TimeUnit;

public class Main {
    public static void main(String[] args) throws Exception {
        new NaiveActor("naive").spawn();
        Strand.sleep(Long.MAX_VALUE);
    }

    static class BadActor extends BasicActor<String, Void> {
        private int count;

        @Override
        protected Void doRun() throws InterruptedException, SuspendExecution {
            System.out.println("(re)starting actor");
            for (;;) {
                String m = receive(300, TimeUnit.MILLISECONDS);
                if (m != null)
                    System.out.println("Got a message: " + m);
                System.out.println("I am but a lowly actor that sometimes fails: - " + (count++));

                if (ThreadLocalRandom.current().nextInt(30) == 0)
                    throw new RuntimeException("darn");

                checkCodeSwap(); // this is a convenient time for a code swap
            }
        }
    }

    static class NaiveActor extends BasicActor<Void, Void> {
        private ActorRef<String> myBadActor;

        public NaiveActor(String name) {
            super(name);
        }

        @Override
        protected Void doRun() throws InterruptedException, SuspendExecution {
            spawnBadActor();

            int count = 0;
            for (;;) {
                receive(500, TimeUnit.MILLISECONDS);
                myBadActor.send("hi from " + self() + " number " + (count++));
            }
        }

        private void spawnBadActor() {
            myBadActor = new BadActor().spawn();
            watch(myBadActor);
        }

        @Override
        protected Void handleLifecycleMessage(LifecycleMessage m) {
            if (m instanceof ExitMessage && Objects.equals(((ExitMessage) m).getActor(), myBadActor)) {
                System.out.println("My bad actor has just died of '" + ((ExitMessage) m).getCause() + "'. Restarting.");
                spawnBadActor();
            }
            return super.handleLifecycleMessage(m);
        }
    }
}

Here we have a NaiveActor spawning an instance of a BadActor, which occasionally fails. Because our naive actor watches its protege, it will be notified of its untimely death, and re-spawn a new one.

In this example, Java is rather annoying, especially when it comes to testing the type of a message with instanceof and casting objects from one type to another. This is much better done in Clojure or Kotlin (I’ll post a Kotlin actor example one day), with their pattern matching. So, yes, all this type-checking and casting is certainly bothersome, and if this type of code encourages you to give Kotlin a try – you should certainly go for it (I have, and I like Kotlin a lot, but it has to mature before it’s fit for use in production). Personally, I find this annoyance rather minimal.

- A crucial component of actor-based fault-tolerant systems, is reducing downtime not only caused by application erros, but also by maintenance. W
- There are several ways to perform actor hot code swapping (e.g. via JMX) now we’ll do it by monitoring the file system. First, create a subdirectory under the project’s directory, which we’ll call modules. Then add the following line to build.gradle’s run section:

systemProperty "co.paralleluniverse.actors.moduleDir", "${rootProject.projectDir}/modules"

Now, in a terminal window, start the program (gradle run, remember?). While the program is running, let’s go back to the editor, and modify our BadActor class a bit:

@Upgrade
static class BadActor extends BasicActor<String, Void> {
    private int count;

    @Override
    protected Void doRun() throws InterruptedException, SuspendExecution {
        System.out.println("(re)starting actor");
        for (;;) {
            String m = receive(300, TimeUnit.MILLISECONDS);
            if (m != null)
                System.out.println("Got a message: " + m);
            System.out.println("I am a lowly, but improved, actor that still sometimes fails: - " + (count++));

            if (ThreadLocalRandom.current().nextInt(100) == 0)
                throw new RuntimeException("darn");

            checkCodeSwap(); // this is a convenient time for a code swap
        }
    }
}

We add the @Upgrade annotation because that’s the class we want to upgrade, and modify the code so that now the actor fails less often. Now, while our original program is still running, let’s rebuild our program’s JAR, by running gradle jar in a new terminal window. For those unfamiliar with Java, JAR (Java Archive) files are used to package Java modules (we’ll discuss modern Java packaging and deployment in part 2). Finally, in that second terminal, copy build/libs/jmodern.jar into our modules directory. In Linux/Mac:

cp build/libs/jmodern.jar modules

You’ll see the running program changing (depending on your OS, this can take up to 10 seconds). Note that unlike when we restarted BadActor after it failed, when we swap the code, its internal state (the value of counter) is preserved.

Designing fault-tolerant applications with actors is a big subject, but I hope you’ve now got a little taste of what’s possible.

# Advanced Topic: Pluggable Types

Before signing off, we’ll venture into dangerous territory. The tool we’ll play with in this section cannot be added to the modern Java developer’s toolbelt just yet, as using it is still too cumbersome, and it would greatly benefit from IDE integration, which is currently very sketchy. Nevertheless, the possibilities it opens are so cool, that if the tool continues to be developed and fleshed out, and if it’s not overused in a frenzy, it might prove invaluable, and that is why it’s included here.

- One of the potentially most powerful (and probably least discussed) new features in Java 8, is **type annotations and pluggable type systems**.
- The Java compiler now allows adding annotations wherever it allows specifying a type (we will shortly see an example). This, combined with the ability to plug annotation processors into the compiler, opens the door to pluggable type systems.
- These optional type systems, that can be turned on and off, can add powerful **type-based static verification** to Java code.
- The Checker framework is a library that allows (advanced) developers write their own pluggable type systems, complete with inheritence, type inference and more. It also comes pre-packaged with quite a few type systems, that verify nullability, tainting, regular expressions, physical units, immutability and more.

I haven’t been able to get Checker to work well with NetBeans, so for this section, we’ll continue without our IDE. First, let’s modify build.gradle a bit. We’ll merge the following:

```java
configurations {
    checker
}

dependencies {
    checker 'org.checkerframework:jdk8:1.8.1'
    compile 'org.checkerframework:checker:1.8.1'
}
into the respective configurations and dependencies sections.

Then, we’ll put this somewhere in the build file:

compileJava {
    options.fork = true
    options.forkOptions.jvmArgs = ["-Xbootclasspath/p:${configurations.checker.asPath}:${System.getenv('JAVA_HOME')}/lib/tools.jar"]
    options.compilerArgs = ['-processor', 'org.checkerframework.checker.nullness.NullnessChecker,org.checkerframework.checker.units.UnitsChecker,org.checkerframework.checker.tainting.TaintingChecker']
}
```

- The last line says that we would like to use Checker’s nullness type system, the physical units type system, and the tainted data type system.

- Now let’s run a few experiments. First, let’s try the nullability type system, which is supposed to prevent null pointer exceptions:

```java
package jmodern;

import org.checkerframework.checker.nullness.qual.*;

public class Main {
    public static void main(String[] args) {
        String str1 = "hi";
        foo(str1); // we know str1 to be non-null

        String str2 = System.getProperty("foo");
        // foo(str2); // <-- doesn't compile as str2 may be null
        if (str2 != null)
            foo(str2); // after the null test it compiles
    }

    static void foo(@NonNull String s) {
        System.out.println("==> " + s.length());
    }
}
```

The Checker framework developers were kind enough to annotate the entire JDK for nullability return types, so you should be able to pass the return value of library methods that never return null as a @NonNull parameter (but I haven’t tried).

Next, let’s try the units type system, supposed to prevent unit conversion errors:

```java
package jmodern;

import org.checkerframework.checker.units.qual.*;

public class Main {
    @SuppressWarnings("unsafe") private static final @m int m = (@m int)1; // define 1 meter
    @SuppressWarnings("unsafe") private static final @s int s = (@s int)1; // define 1 second

    public static void main(String[] args) {
        @m double meters = 5.0 * m;
        @s double seconds = 2.0 * s;
        // @kmPERh double speed = meters / seconds; // <-- doesn't compile
        @mPERs double speed = meters / seconds;

        System.out.println("Speed: " + speed);
    }
}
```

Cool. According to the Checker documentation, you can also define your own physical units.

- Finally, let’s try the tainting type system, which helps you track tainted (potentially dangerous) data obtained, say, as a user input:

```java
package jmodern;

import org.checkerframework.checker.tainting.qual.*;

public class Main {
    public static void main(String[] args) {
        // process(parse(read())); // <-- doesn't compile, as process cannot accept tainted data
        process(parse(sanitize(read())));
    }

    static @Tainted String read() {
        return "12345"; // pretend we've got this from the user
    }

    @SuppressWarnings("tainting")
    static @Untainted String sanitize(@Tainted String s) {
        if(s.length() > 10)
            throw new IllegalArgumentException("I don't wanna do that!");
        return (@Untainted String)s;
    }

    // doesn't change the tainted qualifier of the data
    @SuppressWarnings("tainting")
    static @PolyTainted int parse(@PolyTainted String s) {
        return (@PolyTainted int)Integer.parseInt(s); // apparently the JDK libraries aren't annotated with @PolyTainted
    }

    static void process(@Untainted int data) {
        System.out.println("--> " + data);
    }
}
```

- Checker gives Java pluggable (can be turned on or off) intersection types (you can have @m int or @m double), with type inference (e.g. a null check turns a @Nullable into a @NonNull), and type annotations can even be added to pre-compiled libraries with the help of a tool. Not even Haskell can do that!

Checker isn’t ready for primetime yet, but when it is, if used wisely, it could become one of the modern Java developer’s most powerful tools.

# Wrapping Up (For Now)

- We’ve seen how with the changes made in Java 8, along with modern tools and libraries, Java bears little resemblance to the Java of old. While the language still shines in large applications, the language and ecosystem now nicely compete with **newer “simple” languages, which are less mature, less tested, less platform-independent, have much smaller ecosystems and almost always poorer performance than Java**.
- We have learned how the modern Java programmer writes code, but we have hardly begun to unleash the full power of Java and the JVM. In particular, we are yet to see Java’s awesome monitoring and profiling tools, or its new, lean, web microframeworks. We will visit those topics in the upcoming blog posts.

- In case you want to get a head start, in part 2 we will be discussing modern Java packaging (with Capsule, which is a little like npm, only much cooler), monitoring and management (with VisualVM, JMX, Jolokia and Metrics), profiling (with Java Flight Recorder, Mission Control, and Byteman), and benchmarking (with JMH). In part 3, we will discuss writing lightweight, scalable HTTP services with Dropwizard and Comsat, Web Actors, and dependency injection with JSR-330.










# An Opinionated Guide to Modern Java, Part 2: Deployment, Monitoring & Management, Profiling and Benchmarking

- In part 1 we presented new Java language features, libraries and tools, that make Java into a much more lightweight development environment: new build tools, easier docs, expressive code and lightweight concurrency.
- In this post, we’ll go beyond the code to discuss Java operations, namely
  - deployment,
  - monitoring and management,
  - profiling and benchmarking.
- Even though the examples will be in Java, most of what we discuss in this post is relevant to all JVM languages as much as it is for Java, the language.

# Preamble

- But before we begin, I’d like to shortly go over some of the responses to the previous post raised by readers, and clarify a couple of things. It turns out that the most contentious recommendation I made in part 1 was the build tool. I wrote, “the modern Java developer uses Gradle”. Some readers took issue with that, and made a good case for Maven. While I personally prefer Gradle’s nice DSL and the ability to use imperative code for non-common build operations, I can understand the preference for the fully declarative Maven, even if it requires lots of plugins. The modern Java developer, then, might prefer Maven to Gradle. I would like to say, though, that in order to use Gradle one does not need to know Groovy, even if one wishes to do some non-standard stuff; I don’t. I just learned a few useful Groovy expressions that I found in Gradle examples online.
- Also, some readers took my use of JUnit and Guava in the example to mean I endorse them. Well, I do. Guava is a very useful library, and JUnit is a fine unit-test framework. TestNG is a fine unit-testing framework as well, but JUnit is so ubiquitous that there is little reason to choose something else, even if another library has some advantages. Also, the unit test example used Hamcrest matchers. One reader pointed me at AssertJ, which looks like a very nice alternative to Hamcrest.

- It is important to understand that this guide is not intended to be comprehensive. There are so many good Java libraries out there that we can’t possibly explore them all. My intention is to give a taste of what’s possible with modern Java.

- Some readers expressed their preference to short Javadoc comments that don’t necessarily fill out all of the fields in the Javadoc “standard form”. For example, this:

```java
/**
 * Returns the result
 */
 int getResult();
is preferable to:

/**
 * This method returns the result.
 * @return the result
 */
 int getResult();
```

- With that I wholeheartedly agree. My example simply demonstrated mixing Markdown with standard Javadoc taglets, and was not intended as a guideline.

- Finally, a few words regarding Android. While Android can execute, via a series of transformations, code written in Java (and perhaps some other JVM languages), **Android is not a JVM, and in fact Android, both officially and in practice, is not Java** (that’s the result of two multinational corporations not being able to reach a licensing agreement). Because Android is not Java, what we covered in part 1 may or may not apply to it, and because Android does not have a JVM, little if anything in this post applies to it.

# Modern Java Packaging and Deployment

- For those of you unfamiliar with the Java ecosystem,
  - Java (or any JVM language) source files, are compiled into .class files (essentially Java binaries), one for each class.
  - The basic mechanism of packaging class files is bundling them (this is normally done by the build tool or IDE) into JAR (Java Archive) files, which are Java binary packages.
    -  JARs are just ZIP files containing class files, and an additional manifest file describing the contents, and possibly containing other information about the distribution (the manifest file also contains the electronic signatures in signed JARs).
    - If you package an application (as opposed to a library) in a JAR, the manifest can point to the app’s main class, in which case the application can be launched with the command `java -jar app.jar`; that’s called an executable JAR.
- Java libraries are packaged into JARs, and then deployed into Maven repositories (those are used by practically all JVM build tools – not just Maven).
  -  Maven repositories manage binaries’ versioning and dependencies (when you request a library from a Maven repository, you can ask for all its transitive dependencies as well).
  - Open source JVM libraries are often hosted at the Central Repository, or other similar public repositories, and organizations manage their own private Maven repositories with tools like Artifactory or Nexus.
  - You can even host your own Maven repository on GitHub.
    - But Maven repos are normally accessed (by your build tool) at build time, and normally host libraries rather than executables.
- Java web applications have traditionally been run in application servers, or servlet containers.
  - Those containers can run multiple web applications, loading and unloading apps on demand.
  - Java web applications are deployed to servlet containers in WAR (Web Archive) files, which are really JARs whose contents are arranged in some standard way, and contain additional configurations.
  - But as far as modern Java is concerned, Java application servers are dead.
- Java desktop applications are often packaged and deployed as platform specific binaries, bundled along with their own JVM.
  - The JDK contains a tool to do just that, and a third-party tool called Packr provides similar functionality.
  - This mechanism is great for desktop apps and games, but not what we want for server software:
    - the packages tend to be very big and require installation by the user.
    - In addition, because they bundle a copy of the JVM, they cannot be patched with security and performance upgrades.
- What we want is a simple, lightweight, fire-and-forget packaging and deployment tool for server-side code. Preferably we would like to take advantage of executable JARs’ simplicity and platform independence.
  - But executable JARs have several deficiencies.
    - Every library is usually packaged into its own JAR, and merging all dependencies into a single JAR, might cause collisions, especially with packaged resources (non-class files).
    - Also, a native library can’t just be dropped into the JAR, and,
    - perhaps most importantly, configuring the JVM (setting heap sizes etc.) falls to the user, and must be done at the command line.
    - Tools like Maven’s Shade plugin or Gradle’s Shadow plugin solve the collision issue, and One-Jar also supports native libraries, but both might interfere with the application in subtle ways, and neither solve the JVM configuration problem.
    - Gradle can bundle the application in a ZIP and generate os-specific launch scripts to configure the JVM, but that approach requires installation, and we can go much more lightweight than that.
    - Also, with a powerful, ubiquitous resource like Maven repositories at our disposal, it would be a shame not to take advantage of them.

- This blog post series is meant to be about how easy and fun it is to work with modern Java (without sacrificing any of it power), but when I looked for a fun, easy and lightweight way to package, distribute and deploy server-side Java apps, I came up empty handed. And so Capsule was born (if you know of any alternatives, please let me know).

# Capsule

Capsule uses the nice platform independence of executable JARs – but without their deficiencies – and (optionally) combines it with the power and convenience of Maven repositories. A capsule is a JAR that contains all or some of the Capsule project’s classes, and a manifest with deployment configuration options. When launched (with a simple java -jar app.jar), the capsule will do all or some of the following: extract the JAR into a cache directory, download and cache Maven dependencies, find an appropriate JVM installation, and configure and run the application in a new JVM process.

Now let’s take Capsule for a spin. We’ll begin with our JModern project that we created in part 1. This is our build.gradle file:

apply plugin: 'java'
apply plugin: 'application'

sourceCompatibility = '1.8'

mainClassName = 'jmodern.Main'

repositories {
    mavenCentral()
}

configurations {
    quasar
}

dependencies {
    compile "co.paralleluniverse:quasar-core:0.5.0:jdk8"
    compile "co.paralleluniverse:quasar-actors:0.5.0"
    quasar "co.paralleluniverse:quasar-core:0.5.0:jdk8"

    testCompile 'junit:junit:4.11'
}

run {
    jvmArgs "-javaagent:${configurations.quasar.iterator().next()}"
}
and here’s our jmodern.Main class:

package jmodern;

import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.strands.Strand;
import co.paralleluniverse.strands.channels.Channel;
import co.paralleluniverse.strands.channels.Channels;

public class Main {
    public static void main(String[] args) throws Exception {
        final Channel<Integer> ch = Channels.newChannel(0);

        new Fiber<Void>(() -> {
            for (int i = 0; i < 10; i++) {
                Strand.sleep(100);
                ch.send(i);
            }
            ch.close();
        }).start();

        new Fiber<Void>(() -> {
            Integer x;
            while((x = ch.receive()) != null)
                System.out.println("--> " + x);
        }).start().join(); // join waits for this fiber to finish
    }
}

To test if our program is working correctly, we’ll try a gradle run.

Now, let’s package it into a capsule. In the build file, we’ll add a capsule configuration. Then, we’ll add the following line to our dependencies:

capsule "co.paralleluniverse:capsule:0.3.1"

There are two basic ways to create a capsule (although you can mix them both). The first is to embed all of the dependencies in the capsule, and the second is to let the capsule download them when first launched. We’ll try the first approach – the “full” capsule – first. We’ll add the following to the bottom of our build file:

task capsule(type: Jar, dependsOn: jar) {
    archiveName = "jmodern-capsule.jar"

    from jar // embed our application jar
    from { configurations.runtime } // embed dependencies

    from(configurations.capsule.collect { zipTree(it) }) { include 'Capsule.class' } // we just need the single Capsule class

    manifest {
        attributes(
            'Main-Class'  : 'Capsule',
            'Application-Class' : mainClassName,
            'Min-Java-Version' : '1.8.0',
            'JVM-Args' : run.jvmArgs.join(' '), // copy JVM args from the run task
            'System-Properties' : run.systemProperties.collect { k,v -> "$k=$v" }.join(' '), // copy system properties
            'Java-Agents' : configurations.quasar.iterator().next().getName()
        )
    }
}

Now let’s build the capsule with gradle capsule, and run it:

java -jar build/libs/jmodern-capsule.jar

If you want to see exactly what Capsule is doing, preface -jar with -Dcapsule.log=verbose, but, because it’s a capsule with embedded dependencies, Capsule will extract the JAR into a cache directory (.capsule/apps/jmodern.Main in the user’s home directory) – the first time it’s run – and then launch a new JVM, configured according to the capsule’s manifest. If you have a Java 7 installation, you can try launching the capsule under Java 7 (by setting the JAVA_HOME environment variable to Java 7’s home directory). Even though it’s launched under Java 7, because the capsule specifies a minimum Java version of 8 (or 1.8, which is the same thing), the capsule will find the Java 8 installation and use it to run our app.

Now for the second approach. We’ll create a capsule with external dependencies. To make the capsule creation easier, we’ll first add a function to our build file (you don’t need to understand it; a Gradle plugin will make this a lot easier – contributions are welcome, BTW – but for now we’ll create the capsule “manually”):

// converts Gradle dependencies to Capsule dependencies
def getDependencies(config) {
    return config.getAllDependencies().collect {
        def res = it.group + ':' + it.name + ':' + it.version +
            (!it.artifacts.isEmpty() ? ':' + it.artifacts.iterator().next().classifier : '')
        if(!it.excludeRules.isEmpty()) {
            res += "(" + it.excludeRules.collect { it.group + ':' + it.module }.join(',') + ")"
        }
        return res
    }
}
Then we’ll change the capsule task in the build file to read:

task capsule(type: Jar, dependsOn: classes) {
    archiveName = "jmodern-capsule.jar"
    from sourceSets.main.output // this way we don't need to extract
    from { configurations.capsule.collect { zipTree(it) } }

    manifest {
        attributes(
            'Main-Class'  :   'Capsule',
            'Application-Class'   : mainClassName,
            'Extract-Capsule' : 'false', // no need to extract the capsule
            'Min-Java-Version' : '1.8.0',
            'JVM-Args' : run.jvmArgs.join(' '),
            'System-Properties' : run.systemProperties.collect { k,v -> "$k=$v" }.join(' '),
            'Java-Agents' : getDependencies(configurations.quasar).iterator().next(),
            'Dependencies': getDependencies(configurations.runtime).join(' ')
        )
    }
}
Now let’s build the new capsule with gradle capsule, and run it again:

java -jar build/libs/jmodern-capsule.jar

The first time it’s run, the capsule will download all of our project’s dependencies into a cache directory, where they will be shared by other capsules using them. Instead of listing the dependencies in the JAR manifest, you can place your project’s pom file (especially useful if you’re using Maven as a build tool), into the capsule’s root. See the Capsule docs for details.

Finally, because this post is applicable to any JVM language, here’s a tiny project packaging a Node.js app in a capsule. The app uses Project Avatar, which allows running Node.js-like JavaScript applications on the JVM. It consists of this source code:

var http = require('http');

var server = http.createServer(function (request, response) {
  response.writeHead(200, {"Content-Type": "text/plain"});
  response.end("Hello World\n");
});
server.listen(8000);
console.log("Server running at http://127.0.0.1:8000/");

And two Gradle build files. One creating a “full” capsule (with embedded dependencies), and the other packaging a capsule with external dependencies. This example demonstrates a capsule with native library dependencies. To build the capsule, run

gradle -b build1.gradle capsule

for a full capsule, or:

gradle -b build2.gradle capsule

for a capsule with external dependencies (the project includes a Gradle wrapper, so you don’t even need Gradle installed to build it; simply type ./gradlew instead of gradle to build).

To run:

java -jar build/libs/hello-nodejs.jar

Project Jigsaw, scheduled for inclusion in Java 9, is intended to fix Java deployment and a host of other issues, like stripped JVM distributions, reduced startup time (this is an interesting talk about Jigsaw). In the meantime, Capsule is a lean, and quite satisfactory solution for modern Java packaging and deployment. Capsule is stateless and installation-free.

# Logging

- Before we get into Java’s more advanced monitoring features, let’s get logging out of the way. Java is known to have a bazillion – give or take – logging libraries, on top of the one built into the JDK. Don’t think about that too much.
- If you need logging, **use SLF4J as the logging API**, period. It’s become the de-facto logging standard, and it has bindings for virtually all logging engines.
- Once you use SLF4J, you can leave the choice of a logging engine for later (you can even pick an engine at deployment time).
- SLF4J chooses a logging engine at runtime, based on whatever relevant JARs are included as dependencies. Most libraries now use SLF4J, and if one of your dependencies doesn’t, SLF4J lets you pipe calls to any logging libraries back to SLF4J, and from there to your engine of choice.
- Speaking of choosing a logging engine, if your needs are simple, pick the JDK’s java.util.logging.
  - For heavy-duty, high-performance logging, pick the Log4j (unless you feel really tied to some other logging engine).

- Let’s add logging to our app. To our dependencies, we’ll add:

```java
compile "org.slf4j:slf4j-api:1.7.7"    // the SLF4J API
runtime "org.slf4j:slf4j-jdk14:1.7.7"  // SLF4J binding for java.util.logging
```

- If we run gradle dependencies we see that our app’s dependencies, in turn, depend on Log4j, which we don’t want for the purpose of this demonstration, add the following line to the build.gradle’s configuration section:

```java
all*.exclude group: "org.apache.logging.log4j", module: "*"
```

- Finally, we’ll add some logging to our code:

```java
package jmodern;

import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.strands.Strand;
import co.paralleluniverse.strands.channels.Channel;
import co.paralleluniverse.strands.channels.Channels;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Main {
    static final Logger log = LoggerFactory.getLogger(Main.class);

    public static void main(String[] args) throws Exception {
        final Channel<Integer> ch = Channels.newChannel(0);

        new Fiber<Void>(() -> {
            for (int i = 0; i < 100000; i++) {
                Strand.sleep(100);
                log.info("Sending {}", i); // log something
                ch.send(i);
                if (i % 10 == 0)
                    log.warn("Sent {} messages", i + 1); // log something
            }
            ch.close();
        }).start();

        new Fiber<Void>(() -> {
            Integer x;
            while ((x = ch.receive()) != null)
                System.out.println("--> " + x);
        }).start().join(); // join waits for this fiber to finish
    }
}
```

- If you now run the app (gradle run), you’ll see the log statements printed to the standard output (that’s the default; we’re not going to get into configuring log files – refer to your logging engine docs for that).
- Both “info” and “warn” logs are printed by default.
  - The logging level can be set in the log configuration (which, again, we’re not going to do now), or at runtime, as we’ll soon see.

# Monitoring and Management with jcmd and jstat

- The JDK includes several command line monitoring and management tools, but here we’ll only shortly cover a couple: jcmd and jstat.
- In order to play with them, we’re going to have to make our app not terminate so quickly, so change the for loop limit in the first fiber from 10 to, say, 1000000, and run it in a terminal with gradle run. In another terminal window, run jcmd. If your JDK is installed correctly and jcmd is on your path, you’ll see something like this:

```
22177 jmodern.Main
21029 org.gradle.launcher.daemon.bootstrap.GradleDaemon 1.11 /Users/pron/.gradle/daemon 10800000 86d63e7b-9a18-43e8-840c-649e25c329fc -XX:MaxPermSize=256m -XX:+HeapDumpOnOutOfMemoryError -Xmx1024m -Dfile.encoding=UTF-8
22182 sun.tools.jcmd.JCmd
```

- It’s a list of all currently running JVM processes. Now, run:

```
jcmd jmodern.Main help
```

- You will see a list of jcmd commands that the particular JVM process supports. Let’s try:

```
jcmd jmodern.Main Thread.print
```

This will print out the current stack trace for all threads running in the JVM. Now try:

```
jcmd jmodern.Main PerfCounter.print
```

- This will print out a long list of various JVM performance counters (you’ll have to Google for their meaning).
- You can now try some of the other commands (like GC.class_histogram).

- jstat is like top for the JVM, only it displays information about GC and JIT activity.
- Suppose our app’s pid is 95098 (you can find it by running jcmd or jps in the shell). Running

```
jstat -gc 95098 1000
```

- Will print GC information every 1000 milliseconds. It will look like this:

```
 S0C    S1C    S0U    S1U      EC       EU        OC         OU       PC     PU    YGC     YGCT    FGC    FGCT     GCT
80384.0 10752.0  0.0   10494.9 139776.0 16974.0   148480.0   125105.4    ?      ?        65    1.227   8      3.238    4.465
80384.0 10752.0  0.0   10494.9 139776.0 16985.1   148480.0   125105.4    ?      ?        65    1.227   8      3.238    4.465
80384.0 10752.0  0.0   10494.9 139776.0 16985.1   148480.0   125105.4    ?      ?        65    1.227   8      3.238    4.465
80384.0 10752.0  0.0   10494.9 139776.0 16985.1   148480.0   125105.4    ?      ?        65    1.227   8      3.238    4.465
```

- The numbers are the current capacity of various GC regions.
  - To learn more about what each means, see the jstat documentation.

- Both jcmd and jstat can connect to JVMs running on remote machines;
  - see their documentation for details (jcmd, jstat).

# Monitoring and Management with JMX

- One of the JVM’s greatest strengths is **how it exposes every single detail of its operation – and that of the standard libraries – for runtime monitoring and management.**
- JMX (Java Management Extensions), is a runtime management and monitoring standard.
  - JMX specifies simple Java objects, called MBeans, that expose monitoring and management operations of the JVM itself, the JDK libraries, and any JVM application.
  - JMX also specifies standard ways of connecting to JVM instances – either locally or remotely – to interact with the MBeans.
  - In fact, jcmd gets much of its information with JMX.
- We will see how to write our own MBeans in the next section, but let’s first see how we can examine the baked-in ones.

- With our app running in one terminal, run `jvisualvm` (included as part of the JDK) in another.
- This will launch `VisualVM`.
  - Before we start playing with it, we need to install some plugins.
    - Go to Tools->Plugins and pick Available Plugins.
    - For the purpose of our demonstration we only need VisualVM-MBeans, but you might as well install all of them except maybe VisualVM-Glassfish and BTrace Workbench).
    - Now pick jmodern.Main in the left pane, and choose the Monitor tab.

- The monitor tab uses information exposed as JMX MBeans about the running JVM and displays them graphically, but we can also manually examine those MBeans (and many more) by choosing the MBeans tab (which will be available only after installing the VisualVM-MBeans plugin), we can examine and interact with all MBeans registered on our JVM instance.
- The one used in the heap plot, for example, is found under java.lang/Memory (double-click the attribute value in order to expand it)
- Now let’s pick the java.util.logging/Logging MBean.
  - The LoggerNames attribute in the right pane, will list all registered logger, including the one we’ve added to our code, jmodern.Main (double-click the attribute value in order to expand it).
- MBeans let us not only inspect monitoring values, but also to set them, and invoke various management operations.
- Pick the Operations tab (in the right pane, next to the Attributes tab).
  - We can now change the logging level at runtime via the JMX MBean. In the setLoggerLevel, fill two values: jmodern.Main in the first, and WARNING in the second (the new logging level)
- Now, when you click the setLoggerLevel button, the “info” log messages will no longer be displayed. If you set the level to SEVERE, both log messages will stop appearing. VisualVM automatically generates this simple GUI without any effort on the developer creating the MBean.
- We can allow VisualVM (and other JMX consoles) to access our app remotely, by adding some system properties. To do that, we add the following lines to our build file’s run section:

```
systemProperty "com.sun.management.jmxremote", ""
systemProperty "com.sun.management.jmxremote.port", "9999"
systemProperty "com.sun.management.jmxremote.authenticate", "false"
systemProperty "com.sun.management.jmxremote.ssl", "false"
(in production, you’d naturally want to enable security).
```

- As we’ve seen, in addition to MBean inspection, VisualVM also has custom monitoring views, some relying on JMX for data and some on other means: it monitors thread state and current stack trace for all threads, it provides insights into the GC and general memory usage, performs and analyzes heap dumps and core dumps, and much, much more.
- VisualVM is one of the most important tools in the modern Java developer’s toolbox.
- A modern Java developer might sometimes prefer a CLI to a nice GUI. A nice project called jmxterm, provides a CLI for JMX MBeans. Unfortunately, it does not yet support Java 7 and 8, but the developer says it will soon (if not, we will release a fix; we already have a working fork).
- The modern Java developer likes REST APIs (if for no other reason that they’re ubiquitous and are easy to build web GUIs for). While the JMX standard supports a few different local and remote connectors, it does not yet include an HTTP connector (it’s supposed to in Java 9). However, a beautiful project called Jolokia fills that void, and gives us RESTful access to our MBeans. Let’s give it a try. Merge the following into the your build.gradle:

## Jolokia

```
configurations {
    jolokia
}

dependencies {
    runtime "org.jolokia:jolokia-core:1.2.1"
    jolokia "org.jolokia:jolokia-jvm:1.2.1:agent"
}

run {
    jvmArgs "-javaagent:${configurations.jolokia.iterator().next()}=port=7777,host=localhost"
}
```

(the fact that Gradle requires a new configuration for each dependency used as a Java agent annoys me to no end. Dear Gradle team: please, please make it easier!).

We also want to have Jolokia in our capsule, so we’ll change the Java-Agents attribute in capsule task to read:

```
'Java-Agents' : getDependencies(configurations.quasar).iterator().next() +
               + " ${getDependencies(configurations.jolokia).iterator().next()}=port=7777,host=localhost",
```

Run the application with gradle run, or with the capsule (gradle capsule; java -jar build/libs/jmodern-capsule.jar), and point your browser at http://localhost:7777/jolokia/version. If Jolokia is working properly, you’ll get a JSON response. Now, to examine our app’s heap usage, do:

curl http://localhost:7777/jolokia/read/java.lang:type\=Memory/HeapMemoryUsage

To change our logger’s log level, you can do:

curl http://localhost:7777/jolokia/exec/java.util.logging:type\=Logging/setLoggerLevel\(java.lang.String,java.lang.String\)/jmodern.Main/WARNING

Jolokia has a very nice HTTP API, that can use both GET and POST operations, and it also allows for secure access. For more information, consult the (excelleny) Jolokia documentation.

An HTTP API opens the door to web management consoles. The Jolokia site has a demo of a Cubism GUI for JMX MBeans. Another project by JBoss, called hawtio uses the Jolokia HTTP API to construct a full featured, browser-based monitoring and manangement console for JVM applications. Aside from being a browser app, hawatio differs from VisualVM in that it is intended as a continuous manitoring/management tool for production code, while VisualVM is more of a troubleshooting tool.

Writing Your Own MBeans
Writing and registering your own MBeans is easy:

package jmodern;

import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.strands.Strand;
import co.paralleluniverse.strands.channels.*;
import java.lang.management.ManagementFactory;
import java.util.concurrent.atomic.AtomicInteger;
import javax.management.MXBean;
import javax.management.ObjectName;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Main {
    static final Logger log = LoggerFactory.getLogger(Main.class);

    public static void main(String[] args) throws Exception {
        final AtomicInteger counter = new AtomicInteger();
        final Channel<Object> ch = Channels.newChannel(0);

        // create and register MBean
        ManagementFactory.getPlatformMBeanServer().registerMBean(new JModernInfo() {
            @Override
            public void send(String message) {
                try {
                    ch.send(message);
                } catch (Exception e) {
                    throw new RuntimeException(e);
                }
            }

            @Override
            public int getNumMessagesReceived() {
                return counter.get();
            }
        }, new ObjectName("jmodern:type=Info"));

        new Fiber<Void>(() -> {
            for (int i = 0; i < 100000; i++) {
                Strand.sleep(100);
                log.info("Sending {}", i); // log something
                ch.send(i);
                if (i % 10 == 0)
                    log.warn("Sent {} messages", i + 1); // log something
            }
            ch.close();
        }).start();

        new Fiber<Void>(() -> {
            Object x;
            while ((x = ch.receive()) != null) {
                counter.incrementAndGet();
                System.out.println("--> " + x);
            }
        }).start().join(); // join waits for this fiber to finish

    }

    @MXBean
    public interface JModernInfo {
        void send(String message);
        int getNumMessagesReceived();
    }
}

We’ve added an MBean that lets us monitor the number of messages received by the second fiber, and also exposes a send operation, that will slip a message into the channel. When we run the app, we can now see our monitored property in VisualVM:

plot it (by double clicking the value):

and use our MBean operation in the Operations tab to sneak a message into the channel:

# Easy Health and Performance Monitoring with Metrics

- Metrics is a cool, modern, library for easy performance and health monitoring, built by Coda Hale back when he was at Yammer.
- It contains common metrics collection and reporting classes like histograms, timers, counters gauges, etc. Let’s take it out for a spin.
- Instead, you’ll need to add the following dependency:

```
compile "com.codahale.metrics:metrics-core:3.0.2"
```

- Metrics can report its metrics via JMX MBeans, write them to CSV files, expose them via a RESTful interface, or publish them to Graphite or Ganglia.
- We will just be reporting to JMX (although we’ll see Metrics’s HTTP reporting in part 3, when we discuss Dropwizard). This will be our new Main class:

```java
package jmodern;

import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.strands.Strand;
import co.paralleluniverse.strands.channels.*;
import com.codahale.metrics.*;
import static com.codahale.metrics.MetricRegistry.name;
import java.util.concurrent.ThreadLocalRandom;
import static java.util.concurrent.TimeUnit.*;

public class Main {
    public static void main(String[] args) throws Exception {
        final MetricRegistry metrics = new MetricRegistry();
        JmxReporter.forRegistry(metrics).build().start(); // starts reporting via JMX

        final Channel<Object> ch = Channels.newChannel(0);

        new Fiber<Void>(() -> {
            Meter meter = metrics.meter(name(Main.class, "messages" , "send", "rate"));
            for (int i = 0; i < 100000; i++) {
                Strand.sleep(ThreadLocalRandom.current().nextInt(50, 500)); // random sleep
                meter.mark(); // measures event rate

                ch.send(i);
            }
            ch.close();
        }).start();

        new Fiber<Void>(() -> {
            Counter counter = metrics.counter(name(Main.class, "messages", "received"));
            Timer timer = metrics.timer(name(Main.class, "messages", "duration"));

            Object x;
            long lastReceived = System.nanoTime();
            while ((x = ch.receive()) != null) {
                final long now = System.nanoTime();
                timer.update(now - lastReceived, NANOSECONDS); // creates duration histogram
                lastReceived = now;
                counter.inc(); // counts

                System.out.println("--> " + x);
            }
        }).start().join(); // join waits for this fiber to finish

    }
}
```

In this example we’ve used a Metrics counter (which counts things), a meter (measures rate of events) and a timer (produces a histogram of time durations). Now let’s run the app and fire up VisualVM.

# Profiling

- **Profiling an application is the key to meeting our performance requirements**.
- Only by profiling can we know which parts of the code affect overall execution speed, and concentrate our efforts to optimize them, and only them.
- Java has always had good profilers, both as part of its IDEs or as separate products. But as a result of merging parts of the JRockit JVM code into HotSpot, Java recently gained its most precise, and lightweight profiler yet.
-  While the tool (or, rather, a combination of two tools), we will explore in this section are not open-source, we discuss them because they are included in the standard Oracle JDK, and are free to use in you development environment (but require a commercial license for use on code deployed to production).

- We will begin with a test program. It’s our original demo with some artificial work added:

```java
package jmodern;

import co.paralleluniverse.fibers.Fiber;
import co.paralleluniverse.strands.Strand;
import co.paralleluniverse.strands.channels.*;
import com.codahale.metrics.*;
import static com.codahale.metrics.MetricRegistry.name;
import java.util.concurrent.ThreadLocalRandom;
import static java.util.concurrent.TimeUnit.*;

public class Main {
    public static void main(String[] args) throws Exception {
        final MetricRegistry metrics = new MetricRegistry();
        JmxReporter.forRegistry(metrics).build().start(); // starts reporting via JMX

        final Channel<Object> ch = Channels.newChannel(0);

        new Fiber<Void>(() -> {
            Meter meter = metrics.meter(name(Main.class, "messages", "send", "rate"));
            for (int i = 0; i < 100000; i++) {
                Strand.sleep(ThreadLocalRandom.current().nextInt(50, 500)); // random sleep
                meter.mark();

                ch.send(i);
            }
            ch.close();
        }).start();

        new Fiber<Void>(() -> {
            Counter counter = metrics.counter(name(Main.class, "messages", "received"));
            Timer timer = metrics.timer(name(Main.class, "messages", "duration"));

            Object x;
            long lastReceived = System.nanoTime();
            while ((x = ch.receive()) != null) {
                final long now = System.nanoTime();
                timer.update(now - lastReceived, NANOSECONDS);
                lastReceived = now;
                counter.inc();

                double y = foo(x);
                System.out.println("--> " + x + " " + y);
            }
        }).start().join();
    }

    static double foo(Object x) { // do crazy work
        if (!(x instanceof Integer))
            return 0.0;

        double y = (Integer)x % 2723;
        for(int i=0; i<10000; i++) {
            String rstr = randomString('A', 'Z', 1000);
            y *= rstr.matches("ABA") ? 0.5 : 2.0;
            y = Math.sqrt(y);
        }
        return y;
    }

    public static String randomString(char from, char to, int length) {
        return ThreadLocalRandom.current().ints(from, to + 1).limit(length)
                .mapToObj(x -> Character.toString((char)x)).collect(Collectors.joining());
    }
}
```

- The function foo does some nonsensical computations, so don’t try to make sense of them. When you run the application (gradle run), you may notice warning from Quasar, that one of the fibers is consuming an inordinate amount of CPU time.
  - To figure out what’s going on, we need to profile.
- The profiler we’ll use is very precise and has a very low overhead. It’s made of two components,
  - The first, Java Flight Recorder is baked into the HotSpot VM.
    - It can record many different JVM events into very efficient buffers.
    - It can be triggered to start and stop recording with jcmd, but we will control it with the second tool.
  - The second tool is Java Mission Control (or JMC), which is included in the JDK installation.
    - JMC was the analog to VisualVM in the JRockit VM, and it performs many of the same functions (like MBean inspection), only it is far uglier.
    - But we will be using JMC for it’s ability to control the Java Flight Recorder, and analyze its recordings (I hope Oracle eventually move this functionality into the much prettier VisualVM).
- Flight Recorder has to be enabled when the program is launched (it won’t record anything yet and won’t affect performance), so we’ll stop the execution, and add this line to build.gradle’s run section:

```
jvmArgs "-XX:+UnlockCommercialFeatures", "-XX:+FlightRecorder"
```

- The UnlockCommercialFeatures flag is necessary because Flight Recorder is a commercial feature, but it’s free for use in development. Now let’s launch the program again.
- In another terminal, let’s fire up Mission Control with the jmc command.
  - In the left pane, right-click jmodern.Main, and choose “Start Flight Recording…”. In the wizard window’s “Event settings” dropbox pick “Profiling - on server”, and click “Next >” (not “Finish”!).
- In the next screen, check the “Heap Statistics” and “Allocation Profiling” boxes, and click “Finish”.
- JMC will now wait for one minute until Flight Recorder concludes the recording. It will then open the recording file for analysis, at which point you can safely terminate our application.
- The “Code” section’s Hot Methods tab immediately uncovers the randomString method as the culprit, responsible for almost 90% of the program’s execution time.
- The Memory section’s Garbage Collection tab shows the heap usage, over the duration of the recording
- And the GC Times tab shows the durtation of the garbage collector’s collections
- We can also examine allocation behavior
- and the heap’s contents
- Java Flight Recorder also has an (unsupported) API that lets us record our own application events in JFR’s recordings.

# Advanced Topic: Profiling and Debugging with Byteman

Like last time, we will conclude this installment with advanced topics. First up is profiling and debugging with Byteman. As we mentioned in part 1, one of the **JVM’s most powerful features is the ability to dynamically load code at runtime** (which goes far beyond loading dynamic libraries in native applications). Not only that: **the JVM gives us the ability to transform, and re-transform, already running code.**

A useful tool which takes advantage of this ability is Byteman by JBoss. **Byteman allows us to inject tracing, debugging and profiling code into a running application**. It is included here as an advanced topic because its support for Java 7, let alone 8, is a bit shaky, and must require fixes (to Byteman, that is). The project is actively developed, but lagging behind. We will therefore use byteman on very basic code.

This will be our main class:

package jmodern;

import java.util.concurrent.ThreadLocalRandom;

public class Main {
    public static void main(String[] args) throws Exception {
        for (int i = 0;; i++) {
            System.out.println("Calling foo");
            foo(i);
        }
    }

    private static String foo(int x) throws InterruptedException {
        long pause = ThreadLocalRandom.current().nextInt(50, 500);
        Thread.sleep(pause);
        return "aaa" + pause;
    }
}

foo simulates calling a service which may take some unknown time to complete.

Next, we’ll merge the following into our build file:

configurations {
    byteman
}

dependencies {
  byteman "org.jboss.byteman:byteman:2.1.4.1"
}

run {
    jvmArgs "-javaagent:${configurations.byteman.iterator().next()}=listener:true,port:9977"
    // remove the quasar agent
}

If you want to test Byteman with a capsule, you can change the Java-Agents attribute in the build file to read:

'Java-Agents' : "${getDependencies(configurations.byteman).iterator().next()}=listener:true,port:9977",

Now, we’ll download Byteman here (we can’t rely only on the dependencies because we’re going to use some of Byteman’s command line tools), unzip the archive, and set the environment variable BYTEMAN_HOME to point to Byteman’s directory.

Now, launch the app in one terminal:

gradle run

It will print something like this:

Calling foo
Calling foo
Calling foo
Calling foo
Calling foo

We want to know how long each call to foo takes, but we’ve forgotten to measure and log that. We’ll use Byteman to insert that log while the program is running.

Start an editor, and create the file jmodern.btm in the project’s directory:

RULE trace foo entry
CLASS jmodern.Main
METHOD foo
AT ENTRY
IF true
DO createTimer("timer")
ENDRULE

RULE trace foo exit
CLASS jmodern.Main
METHOD foo
AT EXIT
IF true
DO traceln("::::::: foo(" + $1 + ") -> " + $! + " : " + resetTimer("timer") + "ms")
ENDRULE

These are Byteman rules, which we will apply to the program. While the program is still running in one terminal, open another, and type:

$BYTEMAN_HOME/bin/bmsubmit.sh -p 9977 jmodern.btm

Our app will now start printing something like this in the first terminal:

Calling foo
::::::: foo(152) -> aaa217 : 217ms
Calling foo
::::::: foo(153) -> aaa281 : 281ms
Calling foo
::::::: foo(154) -> aaa282 : 283ms
Calling foo
::::::: foo(155) -> aaa166 : 166ms
Calling foo
::::::: foo(156) -> aaa160 : 161ms

To see which rules are applied:

$BYTEMAN_HOME/bin/bmsubmit.sh -p 9977

Finally, to unload our Byteman script:

$BYTEMAN_HOME/bin/bmsubmit.sh -p 9977 -u

And now our injected log messages are gone!

Byteman is an extremely powerful tool, made possible by the JVMs flexible code transformations. You can use it to examine variables, log events (either to the standard output or to a file), insert delays and more. You can even easily add your own Byteman actions (say, if you want to log events using your logging engine). For more information, please refer to the Byteman documentation.

# Advanced Topic: Benchmarking with JMH

- Advances in both hardware architecture as well as compiler technology have made benchmarking the only viable way to reason about code performance.
- Modern CPUs (and modern compilers) are so clever that creating a mental performance profile of our code – like game programmers did until the end of the 90s – is damn-near impossible; even for a program written in C; heck, even for a program written in Assembly.
- On the other hand, the cleverness of compilers and CPUs are exactly what makes micro-benchmarking (benchmarking small snippets of code) so hard, **as execution speed is very dependent on context** (for example. it is affected by the state of the CPU cahce, which, in turn, is affected by what other threads are doing).
- Microbenchmarking JVM programs is doubly tricky because,the JVM’s JIT is a profile-guided optimizing compiler, which is very much affected by the context in which code is run.
- Therefore, code in a microbenchmark can be much faster, or much slower, than the same code in the context of a larger program.

- JMH is an open-source Java benchmarking harness by Oracle, that runs code snippets in just the right way so you can truly reason about their performance. - There is another, older tool, called Caliper, which was made by Google to serve the same purpose as JMH, but it is far cruder, and might even give wrong results. Don’t use it.

- We will take JMH for a spin right away, but first the usual warning regarding microbenchmarks:
  - premature optimization is the root of all evil.
  - There’s is no point in benchmarking two algorithms or data structures to find out that one is 100 times faster than the other, if the algorithm accounts for a grand total of 1% of your app’s execution time.
  - Even making that algorithm run infinitely fast would only save your 2%. Benchmark only after you’ve profiled your application and determined which bits would generate the most gain if accelerated.

As always, we’ll begin with the build file. Add these to your dependencies:

testCompile 'org.openjdk.jmh:jmh-core:0.8'
testCompile 'org.openjdk.jmh:jmh-generator-annprocess:0.8'

and put this bench task at the bottom of the build file:

task bench(type: JavaExec, dependsOn: [classes, testClasses]) {
    classpath = sourceSets.test.runtimeClasspath // we'll put jmodern.Benchamrk in the test directory
    main = "jmodern.Benchmark";
}

Finally, we’ll put our benchmark code in src/test/java/jmodern/Benchmark.java. I mentioned 90s game programmers before, and in order to show that some of their techniques still work, we’ll benchmark a “standard” inverse square-root computation, with the fast inverse square root algorithm, misattributed to John Carmack:

package jmodern;

import java.util.concurrent.TimeUnit;
import org.openjdk.jmh.annotations.*;
import org.openjdk.jmh.profile.*;
import org.openjdk.jmh.runner.Runner;
import org.openjdk.jmh.runner.options.OptionsBuilder;
import org.openjdk.jmh.runner.parameters.TimeValue;

@State(Scope.Thread)
@BenchmarkMode(Mode.AverageTime)
@OutputTimeUnit(TimeUnit.NANOSECONDS)
public class Benchmark {
    public static void main(String[] args) throws Exception {
        new Runner(new OptionsBuilder()
                .include(Benchmark.class.getName() + ".*")
                .forks(1)
                .warmupTime(TimeValue.seconds(5))
                .warmupIterations(3)
                .measurementTime(TimeValue.seconds(5))
                .measurementIterations(5)
                .build()).run();
    }

    private double x = 2.0; // prevent constant folding

    @GenerateMicroBenchmark
    public double standardInvSqrt() {
        return 1.0/Math.sqrt(x);
    }

    @GenerateMicroBenchmark
    public double fastInvSqrt() {
        return invSqrt(x);
    }

    static double invSqrt(double x) {
        double xhalf = 0.5d * x;
        long i = Double.doubleToLongBits(x);
        i = 0x5fe6ec85e7de30daL - (i >> 1);
        x = Double.longBitsToDouble(i);
        x = x * (1.5d - xhalf * x * x);
        return x;
    }
}

By the way, like the Checker framework we discussed in part 1, JMH uses an annotation processor. Unlike Checker, JMH does it right, so you get automatic IDE integration with all IDEs. Here for example, is what happens in NetBeans if you forget to include the @State annotation

To run the benchmarks, type gradle bench at the shell. I got these results:

Benchmark                       Mode   Samples         Mean   Mean error    Units
j.Benchmark.fastInvSqrt         avgt        10        2.708        0.019    ns/op
j.Benchmark.standardInvSqrt     avgt        10       12.824        0.065    ns/op

Nice, but keep in mind that fast-inv-sqrt is a rough approximation, good only to a few decimal places.

Here’s another example, this one also reports the time spent garbage-collecting, and gives a crude method stack profile:

package jmodern;

import java.util.*;
import java.util.concurrent.*;
import org.openjdk.jmh.annotations.*;
import org.openjdk.jmh.profile.*;
import org.openjdk.jmh.runner.Runner;
import org.openjdk.jmh.runner.options.OptionsBuilder;
import org.openjdk.jmh.runner.parameters.TimeValue;

@State(Scope.Thread)
@BenchmarkMode(Mode.AverageTime)
@OutputTimeUnit(TimeUnit.NANOSECONDS)
public class Benchmark {
    public static void main(String[] args) throws Exception {
        new Runner(new OptionsBuilder()
                .include(Benchmark.class.getName() + ".*")
                .forks(2)
                .warmupTime(TimeValue.seconds(5))
                .warmupIterations(3)
                .measurementTime(TimeValue.seconds(5))
                .measurementIterations(5)
                .addProfiler(GCProfiler.class)    // report GC time
                .addProfiler(StackProfiler.class) // report method stack execution profile
                .build()).run();
    }

    @GenerateMicroBenchmark
    public Object arrayList() {
        return add(new ArrayList<>());
    }

    @GenerateMicroBenchmark
    public Object linkedList() {
        return add(new LinkedList<>());
    }

    static Object add(List<Integer> list) {
        for (int i = 0; i < 4000; i++)
            list.add(i);
        return list;
    }
}

Here is an example of the profiling info printed by JMH:

Iteration   3: 33783.296 ns/op
          GC | wall time = 5.000 secs,  GC time = 0.048 secs, GC% = 0.96%, GC count = +97
             |
       Stack |  96.9%   RUNNABLE jmodern.generated.Benchmark_arrayList.arrayList_AverageTime_measurementLoop
             |   1.8%   RUNNABLE java.lang.Integer.valueOf
             |   1.3%   RUNNABLE java.util.Arrays.copyOf
             |   0.0%            (other)
             |

JMH is a very rich framework. Unfortunately, it is a little thin on documentation, but it does have a rather nice tutorial (which also demonstrates the pitfalls of naive Java microbenchmarking) written as a series of code samples. You can also read this good introductory post by Nitsan Wakart.

# So, What Have We Learned So Far?

- In this post we’ve covered some of the best tools for JVM management, monitoring and profiling.
- The JVM is very serious about providing deep insight into its operation, which is, in addition to its great performance,
  - the main reason I wouldn’t replace the JVM as the platform for a heavy duty, long-running server-side app, with any other technology.
  - We’ve also seen how powerful the JVM is when it comes to modifying running code with tools like Byteman.

- We’ve also introduced Capsule, a lightweight, single-file, stateless, installation-free deployment package for JVM apps. It optionally supports automatic upgrades – for the entire app, or just a library dependency – via a public, or organizational Maven repository.




# An Opinionated Guide to Modern Java, Part 3: Web Development

After playing with modern Java code in part 1, and exploring deployment, management, monitoring and benchmarking of JVM applications in part 2, it is time to delve into modern Java web development.

# Preamble

- Last week we’ve seen how the JVM takes monitoring seriously, and how it exposes every aspect of its runtime behavior.
- One of the readers mentioned a tool, which I’ve had the pleasure to use a few times but neglected to mention it in last week’s installment. This tool, **JITWatch**, it is called, helps to analyze the deepest reaches of the JVM, and is therefore only recommended to the most performance-conscious expert Java (or other JVM language) developers.
  - It takes the output logs generated by adding these JVM options – ``-XX:+UnlockDiagnosticVMOptions -XX:+TraceClassLoading -XX:+LogCompilation -XX:+PrintAssembly` – and turns them into explorable insight into how, and when, the JVM optimizes your code.
  - It shows which methods are compiled to machine code (it even displays the generated machine code if the `-XX:+PrintAssembly` is available, on certain JVM builds), which are inlined, why certain methods have not been inlined, and much, much more.
  - Usage information, as well as screenshots, can be found on the project’s wiki.

- Some readers have opined that Capsule is somehow less standard than OS packages. This is not true, as capsules are stateless executables, and require no installation whatsoever; as such, they don’t even perform the same function as OS packages, which standardize installation. If your application requires some stateful installation (i.e., installation that requires user-guided configuration at install time), then Capsule is not for you. Others have expressed concern over capsules relying on the availability of a Maven repository at runtime. To this I say that, obviously, software comes at different points on an availability/”mission-criticalness” spectrum, and different applications might choose different tradeoffs when it comes to safety vs. convenience. You can create a capsule with no support for automatic upgrades, or a capsule with no external dependencies at all (and embed all dependencies directly in the capsule). You’ll still get automatic choice of a Java runtime and automatic JVM configuration when you launch the capsule. If you do choose to use external Maven dependencies, I think that there is no reason to suspect accidental inclusion of a wrong dependency version – or other such mishaps – any more than when dependency resolution is done at build time. On the contrary: in the former case, the dependencies are explicitly specified in the capsule, and the capsule can be asked to print out its entire dependency tree. Also, if your organization’s Maven release repository is used as a host for capsule artifacts, there is no reason not to treat it as a devops server, and make sure that it’s as available as other servers needed at runtime (especially because Maven repository software isn’t particularly known to crash).

# Introduction to Modern Java Web Development

- Because Java web servers are about as old as the web itself, and there are long, successful, traditions and practices associated with them – traditions which we will soon commence on dismantling – this is perhaps as good a time as any to explain what I mean by “modern” in this series’s title.
- In this context, I take “modern” to mean “in accordance with current general software development trends”.
  - These trends aren’t completely arbitrary, and they are consistent with one another.
  - The birth of a very large number of small, young, fast-moving startups, has given rise to a preference of lean development approaches.
    - Those require easier onboarding, fewer installation, deployment and configuration steps, and a convergence of the roles of development and operations.
  - The growing popularity of the cloud encourages certain approaches towards resource management, namely virtualization, either at the hypervisor level or the OS level.
  - OS-level deployment/resource allocation also supports the proliferation of polyglot architectures, which seek to use the right (but possibly different) tool for each job.
- Traditional Java web servers – or, in their full-featured incarnation, application servers – have one particular distinguishing feature:
  - the ability to run multiple applications in a single JVM instance.
  - They provide a runtime that is separate from the application.
  - It is upgraded, and installed separately.
  - It can be launched separately.
  - Applications are deployed to a fully configured, possible already running, runtime.
  - While this approach has worked well for quite some time – and you may have good reasons to continue employing it – it is far from modern.
  - Allocating resources among the different applications occupying the server is not simple (if possible at all), and it is certainly incompatible with current trends of using hypervisor- and OS containers to host applications.
  - Tools and techniques designed for hypervisor/OS containers are not effective with multi-app servers. Even if these servers are used to host a single application, their operation is most certainly not modern: installing and configuring the web- or app- server is usually not trivial, and deploying applications to said servers take multiple steps, and may be cumbersome.
- The modern approach, that used by practically all other languages and runtime platforms, and increasingly adopted in the Java world, is that of the single-app server.
  - In this kind of server, the web container is embedded in the application (rather than the application being deployed to a web container).
  - This allows for simple deployment, management and configuration, and resource allocation at the OS/hypervisor level.
  - This is why, when modern Java is concerned, application servers (and by that I mean any servlet or full-featured Java EE server designed to run more than one application) – are dead.
- Now, the tools and techniques we will survey here are far from comprehensive. Especially when it comes to web, and web-related, development, tools, libraries and frameworks proliferate.
  - Part of the reason for that is that, unlike fields such as embedded development or mainframe applications, web development is popular among all those fast-moving startups I mentioned, as well as hobbyists.
  - These populations are early adopters and like to experiment with new techniques and invent new ones – sometimes in order to get some technological edge, sometimes for learning purposes, and sometimes for more gratuitous self gratification.
  - The outcome is hundreds of libraries, all achieving similar goals, but in slightly different ways. This happens in the Java world, just as it does in other language ecosystems.
- Also, we will not discuss “full” web frameworks at all, and by that I mean large MVC frameworks, template systems, or any framework designed for applications that render HTML on the server.
  - There are a few reasons for that:
    - One, I’ve never used any of those, so I certainly cannot comment on their suitability or “modernness”;
    - two, the topic is a complex one, requires much discussion, and has been done elsewhere ;
      - https://www.youtube.com/watch?v=ygW8fJVlDxQ
      - https://web.archive.org/web/20180621141839/https://zeroturnaround.com/rebellabs/the-curious-coders-java-web-frameworks-comparison-spring-mvc-grails-vaadin-gwt-wicket-play-struts-and-jsf/
    - three, it seems like web development is moving towards client-side rendering and “single-page apps” (with client side frameworks like Angular et al.), essentially adopting an architecture similar to old client-server apps, and relying on HTTP services to transfer data and commands to and from the server.
      - That transition is not complete – in particular, it depends on mobile phone browsers improving their JavaScript performance – but it is near certain that we’ll be seeing less and less HTML generated dynamically on the server.
  - We will, therefore, only discuss frameworks and libraries for HTTP “data” services.

# HTTP Services with JAX-RS and Dropwizard

- One of the things setting Java apart from other languages is the work of the JCP (Java Community Process), whose work it is to specify standard APIs (even for libraries not part of the language specification or even of the standard runtime library), which are then implemented by various commercial or open-source projects.
- These **JSRs (Java Specification Requests)**, are made by expert groups, and are often known to take an eternity to fully mature and become a standard.
  - But when JSRs are successful, they are very useful as almost all libraries catering to the related field, would implement the standard API, which makes switching implementations, if not trivial than at least less painful.
- Standards are more important for server implementation (where the framework is much more pervasive in the code), than for clients (where each call is more-or-less independent and can be replaced).
- You can use three different HTTP clients, and 3 different JDBC APIs in the same method, but your server usually runs on a single framework.
  - For that reason, you should prefer a standard server API over a non-standard one, unless the non-standard one gives you some very substantial advantages, or otherwise fits your particular use case significantly better. Mere API aesthetics should not sway you in favor of a non-standard API.
- A lightweight web-service server, then, should best implement the standard APIs.
  - When it comes to HTTP services, there are a couple of pertienent APIs.
    - The first is the **good-old Servlet API (currently under JSR-315 for Servlet 3.0, and JSR-340, for Servlet 3.1**).
    - Almost all Java web servers implement the Servlet API, some of them are “modern” (in the sense we discussed earlier), the most popular of which is Jetty.
    - Unlike traditional Java web servers, Jetty is not a standalone web-app container, but a web-server library embedded in the application.
    - It was built to be modern. But even more traditional web servers, like Tomcat, now have modern embedded modes.
    - Because Servlets are a relatively low-level HTTP server API, we won’t be directly working with them here, so let’s move on to the next standard API, **JAX-RS (currently, in version 2.0, specified in JSR-339)**. There are several implementations of JAX-RS, like Apache CXF, RESTEasy and Restlet, but the most popular one seems to be Jersey.
- A JAX-RS implementation is usually used by applying it on top of a Servlet server.
  - It would therefore be natural to build a modern Java web service microframework by putting together Jetty and Jersey, and that’s pretty much the tool we’ll be playing with next: **Dropwizard**.

# Dropwizrd

- So Dropwizard takes Jetty, Jersey, a JSON library called Jackson, Metrics – the modern performance monitoring library (which happens to have been created by Coda Hale, the man behind Dropwizard) – and a bunch of other libraries, and combines them into a complete, simple, modern Java web service microframework.
- We’ll now write our first modern Java web service with Dropwizard.
- We’ll create a new jmodern-web directory, cd into it, and create a Gradle project with `gradle init --type java-library`,
  - and delete the stub source files Gradle creates (src/main/java/Library.java and src/test/java/LibraryTest.java).
- Then, we’ll edit build.gradle to say:

```java
apply plugin: 'java'
apply plugin: 'application'

sourceCompatibility = '1.8'

mainClassName = 'jmodern.Main'
version = '0.1.0'

repositories {
    mavenCentral()
}

configurations {
    capsule
}

dependencies {
    compile 'io.dropwizard:dropwizard-core:0.7.0'
    capsule 'co.paralleluniverse:capsule:0.4.0'
    testCompile 'junit:junit:4.11'
}

task capsule(type: Jar, dependsOn: classes) {
    archiveName = "jmodern-web.jar"

    from jar // embed our application jar
    from { configurations.runtime } // embed dependencies

    from(configurations.capsule.collect { zipTree(it) }) { include 'Capsule.class' } // we just need the single Capsule class

    manifest {
        attributes(
            'Main-Class'  :   'Capsule',
            'Application-Class'   : mainClassName,
            'Application-Version' : version,
            'Min-Java-Version' : '1.8.0',
            'JVM-Args' : run.jvmArgs.join(' '),
            'System-Properties' : run.systemProperties.collect { k,v -> "$k=$v" }.join(' '),
        )
    }
}
```

- Our src/main/java/jmodern/Main.java file would be:

```java
package jmodern;

import io.dropwizard.Application;
import io.dropwizard.*;
import io.dropwizard.setup.*;
import java.util.*;
import java.util.concurrent.atomic.AtomicLong;
import javax.ws.rs.*;
import javax.ws.rs.core.*;

public class Main extends Application<Configuration> {
    public static void main(String[] args) throws Exception {
        new Main().run(new String[]{"server"});
    }

    @Override
    public void initialize(Bootstrap<Configuration> bootstrap) {
    }

    @Override
    public void run(Configuration configuration, Environment environment) {
        environment.jersey().register(new HelloWorldResource());
    }

    @Path("/hello-world")
    @Produces(MediaType.APPLICATION_JSON)
    public static class HelloWorldResource {
        private final AtomicLong counter = new AtomicLong();

        @GET
        public Map<String, Object> sayHello(@QueryParam("name") String name) {
            Map<String, Object> res = new HashMap<>();
            res.put("id", counter.incrementAndGet());
            res.put("content", "Hello, " + (name != null ? name : "World"));
            return res;
        }
    }
}
```
- This is pretty much the simplest Dropwizard service possible. The sayHello method returns a map, which is automatically changed into a JSON object.
- To run this, type gradle run at the shell, or build a capsule first with gradle capsule and run it with `java -jar build/libs/jmodern-web.jar`.
- To test the service point your browser at http://localhost:8080/hello-world, and then at http://localhost:8080/hello-world?name=Modern+Developer.

- Now let’s improve our service a bit by taking advantage of other Dropwizard features:

```java
package jmodern;

import com.codahale.metrics.*;
import com.codahale.metrics.annotation.*;
import com.fasterxml.jackson.annotation.*;
import com.google.common.base.Optional;
import io.dropwizard.Application;
import io.dropwizard.*;
import io.dropwizard.setup.*;
import java.util.concurrent.ThreadLocalRandom;
import java.util.concurrent.atomic.AtomicLong;
import javax.ws.rs.*;
import javax.ws.rs.core.*;
import org.hibernate.validator.constraints.*;

public class Main extends Application<Main.JModernConfiguration> {
    public static void main(String[] args) throws Exception {
        new Main().run(new String[]{"server", System.getProperty("dropwizard.config")});
    }

    @Override
    public void initialize(Bootstrap<JModernConfiguration> bootstrap) {
    }

    @Override
    public void run(JModernConfiguration cfg, Environment env) {
        JmxReporter.forRegistry(env.metrics()).build().start(); // Manually add JMX reporting (Dropwizard regression)

        env.jersey().register(new HelloWorldResource(cfg));
    }

    // YAML Configuration
    public static class JModernConfiguration extends Configuration {
        @JsonProperty private @NotEmpty String template;
        @JsonProperty private @NotEmpty String defaultName;

        public String getTemplate()    { return template; }
        public String getDefaultName() { return defaultName; }
    }

    // The actual service
    @Path("/hello-world")
    @Produces(MediaType.APPLICATION_JSON)
    public static class HelloWorldResource {
        private final AtomicLong counter = new AtomicLong();
        private final String template;
        private final String defaultName;

        public HelloWorldResource(JModernConfiguration cfg) {
            this.template = cfg.getTemplate();
            this.defaultName = cfg.getDefaultName();
        }

        @Timed // monitor timing of this service with Metrics
        @GET
        public Saying sayHello(@QueryParam("name") Optional<String> name) throws InterruptedException {
            final String value = String.format(template, name.or(defaultName));
            Thread.sleep(ThreadLocalRandom.current().nextInt(10, 500));
            return new Saying(counter.incrementAndGet(), value);
        }
    }

    // JSON (immutable!) payload
    public static class Saying {
        private long id;
        private @Length(max = 10) String content;

        public Saying(long id, String content) {
            this.id = id;
            this.content = content;
        }

        public Saying() {} // required for deserialization

        @JsonProperty public long getId() { return id; }
        @JsonProperty public String getContent() { return content; }
    }
}
```

- We’ve made a few improvement.
  - First, the JSON object is now modeled as an immutable Java class.
  - Second, we’ve added a random sleep to our service, and the @Timed anontation, which will automatically monitor and report its latency with the Metrics library.
  - Finally, we’ve made our HelloWorld service configurable, using DropWizard YAML configuration.
- While this is probably excessive for a simple “Hello, World” service, this serves as the basis for much more robust applications.
  - The extra code has bought us monitoring, configurability and type safety.
- To create the configuration we’ll need to create a configuration class, and made a couple of changes to our build file.
- The file src/main/resurces/jmodern.yml will contain our configuration:
```yml
template: Hello, %s!
defaultName: Stranger
```

- Next, add this to build.gradle so that when we run the server with gradle run, it will locate the config file:

```java
run {
    systemProperty "dropwizard.config", "build/resources/main/jmodern.yml"
}
```

- Finally, we want to include the default configuration file in the capsule, so to the capsule section we’ll add:

```
from { sourceSets.main.resources }
```

and we’ll change the System-Properties manifest attribute to use our config file by default:

```
'System-Properties' : (run.systemProperties + ["dropwizard.config": '$CAPSULE_DIR/jmodern.yml']).collect { k,v -> "$k=$v" }.join(' '),
```

- We’ll now build our deployment capsule with gradle capsule, and launch the server with java -jar build/libs/jmodern-web.jar.
- You can now test our improved service browser at http://localhost:8080/hello-world, and http://localhost:8080/hello-world?name=Modern+Developer.

- What if we want to override the default?
  - Create the following foo.yml file in the project’s directory:

```yml
template: Howdy, %s!
defaultName: fella
```

- To use the new configuration, we override the dropwizard.config system property:

```
java -Ddropwizard.config=foo.yml -jar build/libs/jmodern-web.jar
```

- We can fire up VisualVM and take a look at  metrics our server reports, and in particular, our service methods timing:
- When we point our browser to port 8081, we see Dropwizard’s admin console:
- Going to http://localhost:8081/metrics, returns all collected metrics as a JSON object:
- And that’s that! The configuration file can also be used to configure a lot of Dropwizard’s internals, set the logging level and more. See the Dropizard documentation for details.

- All in all, Dropwizard is a lean, fun, modern microframework, that gives you simple deployment, easy configuration, and superb monitoring out of the box. - Another, library with a similar goal is Spring Boot. Unfortunately, Boot does not use the JAX-RS standard API, but there’s a project that seeks to rectify that.

- Dropwizard has a great out-of-the-box experience, but more advanced users might find it confining (some of Dropwizard’s components are hard to replace with others: its choice of a logging engine, for example).
- Those users might find it worthwhile to assemble Jersey, Jetty and other libraries of their choosing, and work out the plumbing themselves, to build a lightweight server that’s the best fit for their organization.
- Doing so should not require a lot of work, and the work necessary is only required once for all of your projects.
- Dropwizard is an excellent starting point, and if it works for you (which it should, in most cases), you can safely stick with it. We will be using Dropwizard for most of the examples in this post, but everything we do is possible using Jetty alone, or combined with Jersey. Dropwizard simply adds simple, consistent configuration and automatic monitoring without little extra work.

# HTTP Clients

- Add the following dependency to the build file:
-
```
compile 'io.dropwizard:dropwizard-client:0.7.0'
```

- Add the following imports to jmodern.Main:

```java
import io.dropwizard.client.*;
import com.sun.jersey.api.client.Client;
```

- and the following two lines to the JModernConfiguration class:

```java
@Valid @NotNull @JsonProperty JerseyClientConfiguration httpClient = new JerseyClientConfiguration();
public JerseyClientConfiguration getJerseyClientConfiguration() { return httpClient; }
```

- We’ll instantiate the client and register a new service, which we’ll call Consumer, in these two lines, added to the run method:

```java
Client client = new JerseyClientBuilder(env).using(cfg.getJerseyClientConfiguration()).build("client");
env.jersey().register(new ConsumerResource(client));
```

- Finally, this will be our consumer service:

```java
@Path("/consumer")
@Produces(MediaType.TEXT_PLAIN)
public static class ConsumerResource {
    private final Client client;

    public ConsumerResource(Client client) {
        this.client = client;
    }

    @Timed
    @GET
    public String consume() {
        Saying saying = client.resource(UriBuilder.fromUri("http://localhost:8080/hello-world").queryParam("name", "consumer").build())
                .get(Saying.class);
        return String.format("The service is saying: %s (id: %d)",  saying.getContent(), saying.getId());
    }
}
```

- Notice how the returned JSON is deserialized into a Saying object;
- it can also be returned as a map, a string, and probably other types as well (Dropwizard is using an outdated version of the Jersey JAX-RS client, but the new API is similar).
- And because Dropwizard supports the Jersey JAX-RS client out-of-the-box, it automatically supplies performance metrics of outgoing requests1.

- To test our new service, start up our application (gradle run, remember) and point your browser at http://localhost:8080/consumer.

- So the JAX-RS standard also specifies a client API.
- But, as we’ve said before, when it comes to client APIs we can let ourselves use non-standard APIs as well.
- An interesting HTTP client API is Retrofit by Square. As you’ve seen, JAX-RS Client can automatically serialize and deserialize Java objects to JSON objects (or XML).
  - Retrofit takes this automatic Java/REST translation (which, BTW, is not always a good thing; domain translations are often particularly leaky abstractions, but they’re helpful if you keep yourself constrained to simple protocols) a step further, and translates the service target URL – not just the payload – to Java interfaces.
  - Unfortunately, Retrofit uses the same annotation names as JAX-RS (server), only defined in a different package, which would make our example a bit ugly. Luckily, Retrofit has a clone/derivatice called Feign, by Netflix.
  - The differences between Feign and Retrofit are not entirely clear to me. Although it seems that Retrofit is more widely adopted (it is older), while Feign is more easily customizable. In any case, the two are extremely similar, and can be used pretty much interchangeably.

- To try Feign out, add the following dependencies to build.gradle:

```java
compile 'com.netflix.feign:feign-core:6.1.2'
compile 'com.netflix.feign:feign-jaxrs:6.1.2'
compile 'com.netflix.feign:feign-jackson:6.1.2'
```

and these imports to Main:

```java
import feign.Feign;
import feign.jackson.*;
import feign.jaxrs.*;
```

- Instead of the JAX-RS client initialization and the consumer service registration in the run method, we’ll create a Feign.Builder:

```java
Feign.Builder feignBuilder = Feign.builder()
        .contract(new JAXRSModule.JAXRSContract()) // we want JAX-RS annotations
        .encoder(new JacksonEncoder()) // we want Jackson because that's what Dropwizard uses already
        .decoder(new JacksonDecoder());
env.jersey().register(new ConsumerResource(feignBuilder));
```

Our consumer service will now look like this:

```java
@Path("/consumer")
@Produces(MediaType.TEXT_PLAIN)
public static class ConsumerResource {
    private final HelloWorldAPI hellowWorld;

    public ConsumerResource(Feign.Builder feignBuilder) {
        this.hellowWorld = feignBuilder.target(HelloWorldAPI.class, "http://localhost:8080");
    }

    @Timed
    @GET
    public String consume() {
        Saying saying = hellowWorld.hi("consumer");
        return String.format("The service is saying: %s (id: %d)",  saying.getContent(), saying.getId());
    }
}
```

Finally, we’ll add the HelloWorldAPI interface, which puts the REST API in Java terms (you can put the interface definition somewhere in our Main class; no need to create a new Java file):

```java
interface HelloWorldAPI {
    @GET @Path("/hello-world")
    Saying hi(@QueryParam("name") String name);

    @GET @Path("/hello-world")
    Saying hi();
}
```

- This interface uses JAX-RS annotations to specify how method calls translate to HTTP requests. The code that actually performs this translation is automatically generated by Feign (or Retrofit).
- After launching our server app, visit http://localhost:8080/consumer to test the new consumer service.

- If you want to see how more complex REST APIs translate to Java, this very simple example demonstrates consuming the GitHub API with Retrofit, and here’s the same example using Feign. Both Retrofit and Feign are very feature-rich, and allow great control over how requests are translated and executed. At this point, I would recommend Retrofit over Feign because Retrofit is more mature, and it makes use of the efficient NIO networking API under the hood, while Feign uses the slow HttpURLConnection API (a better transport mechanism could be plugged into Feign, but I haven’t found any).

- There are other, **lower level HTTP client APIs** (like Apache HTTP Client, which is also directly supported by Dropwizard), but in most circumstances, the higher-level APIs we’ve tried – JAX-RS Client or Retorfit/Feign – work best.

# Database Access

- The JDK includes a standard API for (relational) database access called JDBC (Java Database Connectivity).
- Practically all SQL databases support JDBC.
- But JDBC is a very low-level API, and can sometimes be tiresome to use.
- Java also has a standard high-level database access API – an ORM API actually – called JPA (Java Persistance API), specified by JSR-220 and JSR-317.
- Well known implementations of JPA include Hibernate, OpenJPA and EclipseLink.
  - Do yourself a big favor and don’t use any of them if you can help it.
  - Not that they don’t work – they most certainly do, and they are all fine implementations – but they’re often more trouble than they’re worth.
  - Full blown ORMs encourage a complex object graph and a complex schema, which often results in extremely complex, automatically generated, SQL statements, which are then hard to optimize.
  - Plus, such complex ORMs are not known for their terrific performance.

- Using JDBC directly is often better, but perhaps the best approach is to use one of the tools we will now present.
  - They are somewhere between the low-level JDBC, and a fullblown ORM.
  - They are not standard, which means each has its own API and there aren’t competing, interchangeable, implementations for a standard one, but as we’ve said, going off the standards path is OK for client APIs.
  - In our examples, we’ll be using the H2 embedded database, in in-memory mode.

## JDBI

- We’ll start off with JDBI, which is also directly supported by Dropwizrd. To use JDBI effectively, you’ll need to trade off optimal schema and simple code, until you get to a nice middle ground (JDBI is not ideal for very complex schemas).

We’ll add these dependencies:

``` java
compile 'io.dropwizard:dropwizard-db:0.7.0'
compile 'io.dropwizard:dropwizard-jdbi:0.7.0'
runtime 'com.h2database:h2:1.4.178'
```

and these imports:

```java
import io.dropwizard.db.*;
import io.dropwizard.jdbi.*;
import org.skife.jdbi.v2.*;
import org.skife.jdbi.v2.util.*;
```

We then need to add a DataSource factory to JModernConfiguration:

```java
@Valid @NotNull @JsonProperty private DataSourceFactory database = new DataSourceFactory();
public DataSourceFactory getDataSourceFactory() { return database; }
```

And the following to the run method, which will connect to the database and register our new DbService:

```java
DBI dbi = new DBIFactory().build(env, cfg.getDataSourceFactory(), "db");
env.jersey().register(new DBResource(dbi));
```

In order to configure the database, we need to add the following to jmodern.yml:

```yaml
database:
  driverClass: org.h2.Driver
  url: jdbc:h2:mem:test
  user: u
  password: p
```

Finally, let’s create our database resource (if you’re finding the code changes hard to follow, the full listing is here):

```java
@Path("/db")
@Produces(MediaType.APPLICATION_JSON)
public static class DBResource {
    private final DBI dbi;

    public DBResource(DBI dbi) {
        this.dbi = dbi;

        try (Handle h = dbi.open()) {
            h.execute("create table something (id int primary key auto_increment, name varchar(100))");
            String[] names = { "Gigantic", "Bone Machine", "Hey", "Cactus" };
            Arrays.stream(names).forEach(name -> h.insert("insert into something (name) values (?)", name));
        }
    }

    @Timed
    @POST @Path("/add")
    public Map<String, Object> add(String name) {
        try (Handle h = dbi.open()) {
            int id = h.createStatement("insert into something (name) values (:name)").bind("name", name)
                    .executeAndReturnGeneratedKeys(IntegerMapper.FIRST).first();
            return find(id);
        }
    }

    @Timed
    @GET @Path("/item/{id}")
    public Map<String, Object> find(@PathParam("id") Integer id) {
        try (Handle h = dbi.open()) {
            return h.createQuery("select id, name from something where id = :id").bind("id", id).first();
        }
    }

    @Timed
    @GET @Path("/all")
    public List<Map<String, Object>> all(@PathParam("id") Integer id) {
        try (Handle h = dbi.open()) {
            return h.createQuery("select * from something").list();
        }
    }
}
```

For those of you who know JDBC, this is both familiar and different. JDBI has a fluent interface, and the operations return Java collections, which are then conveniantly and automatically serialized to JSON objects. All in all, this is like a fun, modern, JDBC.

Fire up the application and point your browser at http://localhost:8080/db/all to see all entries, or at http://localhost:8080/db/item/2 to see the second entry. Then, you can also a new entry by entering curl --data Velouria http://localhost:8080/db/add

JDBI can also go a step further, and just like Retrofit, provide us with a custom interface tailored to our DB usage. We’ll even get a bit tricker, by mapping table rows to Java objects.

This will be our domain object (full code listing is here)

```java
public static class Something {
    @JsonProperty public final int id;
    @JsonProperty public final String name;

    public Something(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

The @JsonProperty annotations will ensure that returning this class from one of our service methods will automatically serialize it as a JSON object, but in order for JDBI to work with Something we also need to create a ResultSetMapper which transforms a JDBC ResultSet into a Something object:

```java
public static class SomethingMapper implements ResultSetMapper<Something> {
    public Something map(int index, ResultSet r, StatementContext ctx) throws SQLException {
        return new Something(r.getInt("id"), r.getString("name"));
    }
}
```

Now, for the fun part. This is our DAO class (or SQL Object in JDBI parlance) – JDBI SQL Object is to the database what Retrofit is for REST:

```java
@RegisterMapper(SomethingMapper.class)
interface ModernDAO {
    @SqlUpdate("insert into something (name) values (:name)")
    @GetGeneratedKeys
    int insert(@Bind("name") String name);

    @SqlQuery("select * from something where id = :id")
    Something findById(@Bind("id") int id);

    @SqlQuery("select * from something")
    List<Something> all();
}
```

And now, our new and improved database resource can be written like this:

```java
@Path("/db")
@Produces(MediaType.APPLICATION_JSON)
public static class DBResource {
    private final ModernDAO dao;

    public DBResource(DBI dbi) {
        this.dao = dbi.onDemand(ModernDAO.class);

        try (Handle h = dbi.open()) {
            h.execute("create table something (id int primary key auto_increment, name varchar(100))");
            String[] names = { "Gigantic", "Bone Machine", "Hey", "Cactus" };
            Arrays.stream(names).forEach(name -> h.insert("insert into something (name) values (?)", name));
        }
    }

    @Timed
    @POST @Path("/add")
    public Something add(String name) {
        return find(dao.insert(name));
    }

    @Timed
    @GET @Path("/item/{id}")
    public Something find(@PathParam("id") Integer id) {
        return dao.findById(id);
    }

    @Timed
    @GET @Path("/all")
    public List<Something> all(@PathParam("id") Integer id) {
        return dao.all();
    }
}
```

JDBI isn’t a full ORM solution: it does not automatically generate SQL statements, nor does it automatically marshal full object graphs, but it does get us to a database access sweet-spot, with a lot less weight than any of the JPA implementations.

When using JDBI, Dropwizard will automatically add a health check (http://localhost:8081/healthcheck) that tests the database connectivity, and instrument our DAO with performance metrics:

## JOOQ

The next database access library we will look at, jOOQ, is similar to JDBI’s fluent API (it doesn’t have an analogous API to JDBI’s SQL objects), but takes a different approach: **it uses chains of method calls, rather than strings, to generate SQL statements** (and it can generate SQL compatible with various database implementations).

We’ll add this dependency

```java
compile 'org.jooq:jooq:3.3.2'
```

and these imports:

```java
import org.jooq.Record;
import org.jooq.RecordMapper;
import static org.jooq.impl.DSL.*;
```

In the run method, we’ll now register our DB resource like so (the full code listing is here):

```java
DataSource ds = cfg.getDataSourceFactory().build(env.metrics(), "db"); // Dropwizard will monitor the connection pool
env.jersey().register(new DBResource(ds));
```

And our new DBResource looks like this:

```java
@Path("/db")
@Produces(MediaType.APPLICATION_JSON)
public static class DBResource {
    private final DataSource ds;
    private static final RecordMapper<Record, Something> toSomething =
            record -> new Something(record.getValue(field("id", Integer.class)), record.getValue(field("name", String.class)));

    public DBResource(DataSource ds) throws SQLException {
        this.ds = ds;

        try (Connection conn = ds.getConnection()) {
            conn.createStatement().execute("create table something (id int primary key auto_increment, name varchar(100))");

            String[] names = { "Gigantic", "Bone Machine", "Hey", "Cactus" };
            DSLContext context = using(conn);
            Arrays.stream(names).forEach(name -> context.insertInto(table("something"), field("name")).values(name).execute());
        }
    }

    @Timed
    @POST @Path("/add")
    public Something add(String name) throws SQLException {
        try (Connection conn = ds.getConnection()) {
            // this does not work
            int id = using(conn).insertInto(table("something"), field("name")).values(name).returning(field("id"))
                       .fetchOne().into(Integer.class);
            return find(id);
        }
    }

    @Timed
    @GET @Path("/item/{id}")
    public Something find(@PathParam("id") Integer id) throws SQLException {
        try (Connection conn = ds.getConnection()) {
            return using(conn).select(field("id"), field("name")).from(table("something"))
                    .where(field("id", Integer.class).equal(id)).fetchOne().map(toSomething);
        }
    }

    @Timed
    @GET @Path("/all")
    public List<Something> all(@PathParam("id") Integer id) throws SQLException {
        try (Connection conn = ds.getConnection()) {
            return using(conn).select(field("id"), field("name")).from(table("something")).fetch().map(toSomething);
        }
    }
}
```

Now, jOOQ does not yet implement DDL (SQL statements like create table), so you’ll notice we’re creating the table using JDBC. That’s OK because jOOQ is implemented as a JDBC wrapper, and requires some JDBC anyway (I haven’t been able to get the add method to work (probably because of the auto-generated primary key). jOOQ people: if you’re reading this, please help).

This example really doesn’t do jOOQ justice, as its greatest strength is the ability to generate classes from your schema, and perform all the operations we’ve done above – and far more complex ones – in a completely typesafe manner. jOOQ is a little too clever for my own tastes, but if your schema is complex, it can be an invaluable tool.

# Dependency Injection

- Dependency injection is one of those programming patterns that, depending on whom you ask, can be said to be invaluable or completely useless.
- I believe that DI can be extremely useful in complex codebases; for simple ones it’s largely unnecessary.
- Java has a simple standard DI API specified by JSR-330. JSR-330 has the following implementations: Spring IoC, Guice, Dagger, Sisu (which builds on top of Guice), and HK2.
  - Each of these is developed by a major company or organization.
  - Given this selection, people are often faced with a paradox of choice. Don’t fear: if you stick to the JSR-330 standard, or deviate slightly, you can change your DI solution at any point.
  - If you want your application to be completely configurable by the user (in the form of XML files2), choose Spring (that’s what why we’ve chosen Spring for Galaxy);
  - if not, then start with Dagger, and only switch to something else if and when it no longer satisfies your needs.


## Dagger

We’re going to take Dagger for a spin. First, let’s add the Dagger dependencies:

```java
compile 'com.squareup.dagger:dagger:1.2.1'
compile 'com.squareup.dagger:dagger-compiler:1.2.1'
```

To keep things uncluttered, we’ll leave only the HelloWorldResource. This time, however, instead of manually creating the service and passing it the configuration object, we’ll use Dagger to read our configuration from the YAML file, and inject them into our service.

This is the service:

```java
@Path("/hello-world")
@Produces(MediaType.APPLICATION_JSON)
public static class HelloWorldResource {
    private final AtomicLong counter = new AtomicLong();
    @Inject @Named("template") String template;
    @Inject @Named("defaultName") String defaultName;

    HelloWorldResource() {
    }

    @Timed // monitor timing of this service with Metrics
    @GET
    public Saying sayHello(@QueryParam("name") Optional<String> name) throws InterruptedException {
        final String value = String.format(template, name.or(defaultName));
        Thread.sleep(ThreadLocalRandom.current().nextInt(10, 500));
        return new Saying(counter.incrementAndGet(), value);
    }
}
```

Note the @Inject and @Named annotations. These are part of the JSR-330 standard, so our service code will remain unchanged no matter which DI tool we use. To actually wire and inject the dependencies we use Dagger specific code. Dagger specifies the dependency wiring configuration in a module class. Here’s ours:

```java
@Module(injects = HelloWorldResource.class)
class ModernModule {
    private final JModernConfiguration cfg;

    public ModernModule(JModernConfiguration cfg) {
        this.cfg = cfg;
    }

    @Provides @Named("template") String provideTemplate() {
        return cfg.getTemplate();
    }

    @Provides @Named("defaultName") String provideDefaultName() {
        return cfg.getDefaultName();
    }
}
```

One of the coolest things about Dagger is that it verifies that all dependencies are satisfied at compile time using an annotation processor.

To obtain a fully configured instance of HelloWorldResource, this is what we put in the run method of our application:

```java
ObjectGraph objectGraph = ObjectGraph.create(new ModernModule(cfg));
env.jersey().register(objectGraph.get(HelloWorldResource.class));
```

You’ll notice that the ModernModule class replicates some of the behavior of JModernConfiguration. It would have been great to simply annotate JModernConfiguration with @Module, and the getTemplate and getDefaultName methods with @Provides. Unfortunately, Dagger forbids subclassing in modules.

# Advanced Topic: Blocking vs. Non-blocking or Synchronous vs. Asynchronous

- At this point we’ll take some time for a more theoretical discussion on blocking vs. nonblocking APIs.
-  A blocking, or synchronous, API is one whose methods block the calling thread until they complete.
  - Of course, the concept of blocking (or nonblocking) only makes sense when these methods can potentially take a long time to complete (say tens of milliseconds to tens of seconds).
- Another type of API, which is often called nonblocking but here we’ll call them semi-blocking (or semi-asynchronous),
  - has methods that don’t block the calling thread for the duration of the operation.
  - They only initiate an operation and return a future object.
  - The future is then used to block and wait for the operation to complete at some other convenient time.
-  Finally, a third type of API, a true non-blocking, or asynchronous, API,
  - also does not block the calling thread. Its methods take an additional parameter – a callback function which is code that will be executed (on some unknown thread) when the operation completes.
- Sometimes, Java APIs mix the last two types, both taking a callback and returning a future.

- Let me put this clearly: asynchronous APIs are always more complicated than blocking APIs
  - (that’s true even using languages and libraries that attempt to make callbacks easier with composable promises, comprehensions, monads, and other functional shenanigans).
  - The problem with asynchronous code is especially bad in languages like Java – and basically all other JVM languages, perhaps with the exception of Clojure – which supports multi-threading, but does not restrict side-effects.
  -  We’ll not get into detail here, but using nonblocking APIs in such languages requires great discipline, and a clear understanding of complex concurrency issues.
  - Blocking APIs have none of these problems.

- Why would anyone use asynchronous APIs over synchronous ones, then?
  - The answer is simple: performance.
  - To delve a little deeper, kernel threads have a non-negligible task switching costs (not to speak of thread stack sizes that can quickly swallow up your RAM, which would be better used to store data caches).
  - Modern web applications often delegate actual processing to myriad services, some do offline map-reduce, others may do some online processing, leaving the main function of the client-facing web server to that of a coordinator:
    - it calls many other services and assembles data from many sources.
    - It hardly does any processing, but it performs lots of IO operations – some can be done in parallel, and others need to be called consecutively.
    -  This means that the web server generates many thread-scheduling events (threads blocking and unblocking) for relatively little CPU “work” done, and the thread scheduling overhead imposed by the operating system become onerous.
    - So people put their code into all sort of unnatural contortions simply to get around the kernel thread scheduling performance hit, and some modern web frameworks/libraries lovingly embrace nonblocking APIs (we haven’t discussed any of them because, as we’ll see, they’re all severely misguided :)).

- This is the wrong approach.
  - In order to get around an unsuitable implementation, people abandon a suitable abstraction (threads), instead of simply fixing the implementation.
  - Lightweight (or user-level) threads – used in Erlang, Go, or on the JVM via the Quasar library – let you use simple, blocking APIs, without any of their performance issues.

- It is a rare occurrence in computer science – usually full of tradeoffs and caveats – that one approach almost always beats another, but this is one:
  - asynchronous code has many disadvantages and absolutely zero advantages relative to synchronous code.
  - Even an imperfect implementation of lightweight threads is leaps and bounds better than asynchronous programming, particularly when the language does not guard against shared state mutations.
  - There are probably some exceptions to this rule (after all, in CS, even the absolute isn’t absolutely so), but they are far fewer than those when a goto statement is recommended.

- Synchronous and asynchronous are duals (each can be transformed into the other using “constant time” transformations), but synchronous is the better abstraction for humans, and I can prove this. Let’s examine two APIs:

```java
interface Sync {
    Object pull();
}
```

and:

```java
interface Async {
    void push(Callback cb);
}

interface Callback {
    void got(Object obj);
}
```

Now let’s implement Async using Sync:

```java
Async syncToAsync(Sync sync) {
    return new Async() {
        public void push(final Callback cb) {
            new Thread(() -> {
                  for(;;)
                      cb.got(sync.pull());
              }).start();
        }
    }
}
```

- Now, in your favorite programming language, implement the opposite, i.e. transform an Async to a Sync. This will be trickier, and will invariably require introducing some intermediate data storage, like a queue or a buffer. Of course, you’ll need to take into account that Callback.got can be called on any thread, so you’ll need to mind your concurrency with that data structure. The transformation from Async to Sync is, therefore, not only less trivial, but introduces unnecessary data storage: unnecessary because it is probably already built into the system (in the form of the IO buffers, for example).
- So Async is trivially implemented using Sync, but the opposite transformation is both wasteful, longer, and requires managing concurrency.
  - Again, this is less of an issue in languages that restrict, or manage, side effects (like Clojure or Haskell).

The Comsat project integrates standard (and non-standard but good) Java web-related API with Quasar fibers (lightweight threads). Comsat’s next release will support the tools discussed in this post (with the possible exceptions of jOOQ and Retrofit/Feign), so that you can write the same simple blocking code, but get all the performance and scalability advantages of obtuse asynchronous code. In a future blog post we’ll show how Comsat lets you keep your code but make your application more scalable and resistent to cascading failures.

# Advanced Topic: Interactive Web Services with Web Actors

- While generally you should stick to standard server APIs, sometimes an alternative provides significant advantages. One of the topics not covered here is that of interactive web services that make use of server-push using WebSocket or SSE (Server Sent Events). While Java’s standard APIs support both, working with WebSockets in particular can cause complex concurrency issues, because the standard Java WebSocket APIs (JSR-356) is asynchronous.
  - This means that WebSocket messages might arrive concurrently with, say HTTP requests from the same user.
  -  And in any event, the asynchronous API requires managing mutable shared state, which sucks. Comsat, therefore, provides an API called Web Actors, which assigns an actor to each user session, which receives – synchronously, i.e. with pull rather than push – all messages from a given web session, and makes state management a cinch. To learn more about Web Actors read the introductory blog post, this post on writing an MMO with web actors, or the Comsat documentation.
