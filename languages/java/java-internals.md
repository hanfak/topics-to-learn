# Java internals

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Java internals](#java-internals)
	- [Links](#links)
	- [compiler](#compiler)
	- [JVM](#jvm)
		- [links](#links)
		- [Byte code](#byte-code)
		- [Class Loader](#class-loader)
	- [JDK](#jdk)
	- [JRE](#jre)
	- [JDK/JRE/JVM](#jdkjrejvm)
	- [Just In Time Compiler](#just-in-time-compiler)
	- [Linker?????](#linker)

<!-- /TOC -->


- Java is a programming language and a platform. Java is a high level, robust, object-oriented and secure programming language.
- Platform:
	- Any hardware or software environment in which a program runs, is known as a platform.
	- Since Java has a runtime environment (JRE) and API, it is called a platform.
- Java Platforms / Editions
	- Java SE (Java Standard Edition)
		- It is a Java programming platform.
		- It includes Java programming APIs such as java.lang, java.io, java.net, java.util, java.sql, java.math etc.
		- It includes core topics like OOPs, String, Regex, Exception, Inner classes, Multithreading, I/O Stream, Networking, AWT, Swing, Reflection, Collection, etc.
	- Java EE (Java Enterprise Edition)
		- It is an enterprise platform which is mainly used to develop web and enterprise applications.
		- It is built on the top of the Java SE platform. It includes topics like Servlet, JSP, Web Services, EJB, JPA, etc.
	- Java ME (Java Micro Edition)
		- It is a micro platform which is mainly used to develop mobile applications.
	- JavaFX
		- It is used to develop rich internet applications. It uses a light-weight user interface API.


## Links

- https://www.javaworld.com/article/2076075/learn-java/core-java-learn-java-from-the-ground-up.html
- https://www.javacodegeeks.com/2018/04/jvm-architecture-execution-engine-in-jvm.html
- https://www.javacodegeeks.com/2018/04/jvm-architecture-overview-of-jvm-and-jvm-architecture.html
- https://www.youtube.com/watch?v=iDypTyErl78
- https://www.javacodegeeks.com/2017/10/introduction-java-virtual-machine-jvm.html


## compiler

- https://www.quora.com/How-does-the-Java-compiler-work


## JVM

- JVM (Java Virtual Machine) is an abstract machine.
- called a virtual machine because it doesn't physically exist. It is a specification that provides a runtime environment in which Java bytecode can be executed
- can run those programs which are written in other languages and compiled to Java bytecode.
- platform dependent because the configuration of each OS is different from each other. However, Java is platform independent.
- There are three notions of the JVM:
	- specification
		- where working of Java Virtual Machine is specified.
		- But implementation provider is independent to choose the algorithm.
		- Its implementation has been provided by Oracle and other companies.
	- implementation
		- Its implementation is known as JRE (Java Runtime Environment).
	- instance.
		- Whenever you write java command on the command prompt to run the java class, an instance of JVM is created.
- JVM performs the following main tasks:
	- Loads code
	- Verifies code
	- Executes code
	- Provides runtime environment
- JVM provides definitions for the:
	-	Memory area
	-	Class file format
	-	Register set
	-	Garbage-collected heap
	-	Fatal error reporting etc

### links

- https://www.quora.com/How-does-JVM-works-internally
- https://www.cubrid.org/blog/understanding-jvm-internals/
- https://www.javacodegeeks.com/2018/05/jvm-architecture-101-get-to-know-your-virtual-machine.html
- https://www.javacodegeeks.com/2018/04/jvm-architecture-overview-of-jvm-and-jvm-architecture.html
- https://www.javacodegeeks.com/2018/04/jvm-architecture-jvm-class-loader-and-runtime-data-areas.html

### Byte code

- https://examples.javacodegeeks.com/core-java/bytecode-primer-java-class-files/

### Class Loader

- https://www.javaworld.com/article/2076075/learn-java/core-java-learn-java-from-the-ground-up.html
- https://www.javaworld.com/article/2077260/learn-java/learn-java-the-basics-of-java-class-loaders.html
- https://www.journaldev.com/349/java-classloader
- https://en.wikipedia.org/wiki/Java_Classloader
- https://stackoverflow.com/questions/2424604/what-is-a-java-classloader
- https://www.javacodegeeks.com/2018/04/jvm-architecture-jvm-class-loader-and-runtime-data-areas.html

## JDK

- acronym for Java Development Kit
- a software development environment which is used to develop Java applications and applets.
- physically exists and contains JRE + development tools.
-  JDK contains a
	- private Java Virtual Machine (JVM) and 
	- a few other resources such as
	- an interpreter/loader (java)
	- a compiler (javac)
	- an archiver (jar)
	- a documentation generator (Javadoc)
	- jconsole

## JRE

- acronym for Java Runtime Environment
- AKA Java RTE
- set of software tools which are used for developing Java applications.
- provide the runtime environment
- implementation of JVM. It physically exists. It contains a set of libraries + other files that JVM uses at runtime

## JDK/JRE/JVM

- https://www.journaldev.com/546/difference-jdk-vs-jre-vs-jvm
- https://self-learning-java-tutorial.blogspot.co.uk/2014/03/difference-between-jre-and-jdk.html

## Just In Time Compiler

- https://self-learning-java-tutorial.blogspot.co.uk/2014/03/jit-compiler.html

## Linker?????

- https://www.developer.com/java/data/understand-jvm-loading-jvm-linking-and-jvm-initialization.html
