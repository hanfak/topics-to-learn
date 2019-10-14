# Cohesion

- Cohesion describes how closely related (or not) pieces of code are to each other.
- Can be high or low
- At the method level, high cohesion would mean that the lines of code within the method come together to perform one small task on a small amount of closely related data or objects.
- At the class level, high cohesion would mean the members (methods, properties, events, etc.) are all closely related to each other and to the overall purpose of the class.
- applies at the namespace level and at the assembly level.
- The worst kind of cohesion is that of “Coincidental Cohesion”,
  - this is code that has been grouped together in a completely arbitrary way with no thought having been put into it.
-  best kind of cohesion is “Functional Cohesion”:
  -  this is where pieces of code are highly related by the task that they perform.
- Other types of cohesion
  - Sequential Cohesion: related by input/output data flows
  - Communicational Cohesion: related by operating on the same set(s) of data
  -  Procedural Cohesion: related by always following the same sequence of execution
  - Temporal Cohesion: related by the points in time when they are used
  - Logical Cohesion: related by some logical category but different by actual nature

Why?

- Easier to understand
- Need to change less often
- More easily usable, reusable, and composable • Easier to unit test
- Easier to make well-named

## Links

- https://codurance.com/software-creation/2016/03/03/cohesion-cornerstone-software-design/
- https://pragprog.com/magazines/2010-12/cohesive-software-design
