# Cohesion

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Cohesion](#cohesion)
	- [What](#what)
	- [Classes](#classes)
	- [Other types of cohesion](#other-types-of-cohesion)
		- [Sequential Cohesion:](#sequential-cohesion)
		- [Communicational Cohesion:](#communicational-cohesion)
		- [Procedural Cohesion:](#procedural-cohesion)
		- [Temporal Cohesion:](#temporal-cohesion)
		- [Logical Cohesion:](#logical-cohesion)
		- [functional:](#functional)
		- [Coincidental:](#coincidental)
	- [Why?](#why)
	- [Measuring](#measuring)
	- [Issues](#issues)
	- [Links](#links)

<!-- /TOC -->

## What

-  Cohesion means completeness with itself.
- Software entities (classes & methods) should have a single responsibilty
  - No God object
- Expression should be concise but it must also be complete
- Cohesion describes how closely related (or not) pieces of code are to each other.
- Can be high or low
- At the method level, high cohesion would mean that the lines of code within the method come together to perform one small task on a small amount of closely related data or objects.
- At the class level, high cohesion would mean the members (methods, properties, events, etc.) are all closely related to each other and to the overall purpose of the class.
- applies at the namespace level and at the assembly level.
- Use of lots of little classes which focuses on a single responsiblity
  - Allows ease of change as the change will occur in only one place
- Chunking concepts and abstracting details, helps with not overloading our minds in understanding the code
- Layers of abstractoin help us see the big picture and how components relate with each other
- This allows us to name the entity when responsibilty is well defined
- With a complex class, we need to abstract details to other classes, we do this via composition. And let the complex class delegate behaviour to the other classes it is composed of.
- Code is easier to understand and find bugs , as each entity is dealing with just one thing
-

## Classes

- They can represnt
  - tangible things - wheel barrow
  - intangible things - checking account
  - ideas
  - processes
  - relationships
- They define behaviour of objects
- The get instantiated at runtime
- They are representations not because of their names But
  - because of what they do, their behaviour
  - Names are important because they give us clues for what a class does


## Other types of cohesion

### Sequential Cohesion:

- related by input/output data flows
- Two modules interact, where one outputs data that becomes the input for the other

### Communicational Cohesion:

- related by operating on the same set(s) of data
- Two modules form a communication chain, where each operates on information and/or contributes to some output.
- For example, add a record to the database and generate an email based on #that information.

### Procedural Cohesion:

- related by always following the same sequence of execution

### Temporal Cohesion:

- related by the points in time when they are used
- Modules are related based on timing dependencies.
- For example, many systems have a list of seemingly unrelated things that must be initialized at system startup

### Logical Cohesion:

- related by some logical category but different by actual nature
- For example, consider a module that converts information from text, serialized objects, or streams. Operations are related, but the functions are quite different.
- ie like a utils class

### functional:

- Every part of the module is related to the other, and the module contains everything essential to function.
-  best kind is “Functional Cohesion”:
  -  this is where pieces of code are highly related by the task that they perform.

### Coincidental:

- this is code that has been grouped together in a completely arbitrary way with no thought having been put into it.
-  The worst kind of cohesion
  - this is code that has been grouped together in a completely arbitrary way with no thought having been put into it.

## Why?

- Easier to understand
- Need to change less often
- More easily usable, reusable, and composable
- Easier to unit test
- Easier to make well-named

## Measuring

- Cyclometric complexity
  - used as proxy for cohesion, if module is too complex, then this can be extracted outer
  - Issues  
    - some times the code is complex in it's nature (essential complexity) and splitting out will make it more complex and less cohesion and the logic dispersed
- LCOM
  - Structure of the code,
    - if all fields are used in a method, then it is fine
    - if fields and methods are separated then they can separated

## Issues

- This can oppose low coupling when aiming for high cohesion
  - Ideally, a cohesive module is one where all the parts should be packaged together,  
    - because breaking them into smaller pieces would require coupling the parts together via calls between modules to achieve useful results
  - Attempting to divide a cohesive module would only result in increased coupling and decreased readability
- Can lead to lots of dependencies when there are lots of small modules needing to communicate, hard to understand and follow flow
- Hard to measure
- If module A has functionality which can be split off to another module B is this correct ?
  - Can lead to high coupling, as the Module B will be dependent on Module A to complete the work
  - should they stay in Module A, but can lead to big modules

## Links

- https://pragprog.com/magazines/2010-12/cohesive-software-design
- https://www.codurance.com/publications/software-creation/2016/03/03/cohesion-cornerstone-software-design
- https://www.quora.com/What-are-the-pros-and-cons-of-cohesion-and-coupling
- https://blog.ttulka.com/how-cohesion-and-coupling-correlate/
