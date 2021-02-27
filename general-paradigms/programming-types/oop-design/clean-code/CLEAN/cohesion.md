# Cohesion

- Software entities (classes & methods) should have a single responsibilty
  - No God object
- Expression should be concise but it must also be complete
- Cohesion describes how closely related (or not) pieces of code are to each other.
- Can be high or low
- At the method level, high cohesion would mean that the lines of code within the method come together to perform one small task on a small amount of closely related data or objects.
- At the class level, high cohesion would mean the members (methods, properties, events, etc.) are all closely related to each other and to the overall purpose of the class.
- applies at the namespace level and at the assembly level.
- The worst kind of cohesion is that of “Coincidental Cohesion”,
  - this is code that has been grouped together in a completely arbitrary way with no thought having been put into it.
-  best kind of cohesion is “Functional Cohesion”:
  -  this is where pieces of code are highly related by the task that they perform.
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
  - Sequential Cohesion: related by input/output data flows
  - Communicational Cohesion: related by operating on the same set(s) of data
  -  Procedural Cohesion: related by always following the same sequence of execution
  - Temporal Cohesion: related by the points in time when they are used
  - Logical Cohesion: related by some logical category but different by actual nature

## Why?

- Easier to understand
- Need to change less often
- More easily usable, reusable, and composable • Easier to unit test
- Easier to make well-named

## Links

- https://pragprog.com/magazines/2010-12/cohesive-software-design
- https://www.codurance.com/publications/software-creation/2016/03/03/cohesion-cornerstone-software-design
