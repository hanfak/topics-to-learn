# Lazy & Eager 

## Evaluation

- An ‘eagerly’ evaluated sequence generates all its values immediately on creation
- A Lazy evaluated sequence, values are only generated when they are requested (on demand)
  - Java Stream.iterate and the C# yield loop
  -  It is this deferred execution that enables the pretence of infinite sequences.

## Initialisation 

### Benefits of Lazy 
- Improved performance: 
  - Lazy initialization can improve performance by delaying the initialization until it's actually needed. This means that objects are only created when they are needed, reducing unnecessary memory allocation and speeding up the program's execution.
- Reduced memory usage: 
  - Lazy initialization only initializes objects when they are needed. This reduces memory usage, as objects that are not needed are not created.
- Simplified code:
  - Lazy initialization can simplify code by reducing the number of initializations that need to be done. This can make code easier to read and understand.
  
### Disadvantage of Lazy 
- Increased complexity:
  - Lazy initialization can add complexity to the code. It requires additional logic to determine when to initialize objects, which can be difficult to implement and maintain.
- Delayed errors:
  - As the init will happen during runtime, this can fail if there is a bug and affect the user, or worse hidden and not known about till much later
- First use has poor performance
  - The first user will need to do the initialisation and this will have a performance hit 
  - This can happen to all users, but if there is caching or object pooling, the performance will improve from subsequent users

### Benefits of eager 
- Simple implementation:
  - Eager initialization is a simple approach to initializing objects. It initializes all objects at startup, making it easy to implement and maintain.
- Fast access time: 
  - Eager initialization ensures that all objects are initialized at startup, which means that they are immediately available for use. This can be beneficial for programs that require fast access to objects.
- Issues are discovered at deployment time
  - Can fix the problem before the user interacts with system

### Disadvantage of eager 
- Wasted memory:
  - Eager initialization initializes all objects, regardless of whether they are needed or not. This can result in wasted memory, as objects that are not used will still take up space in memory.
- Slower startup time: 
  - Eager initialization can slow down startup time, as all objects need to be initialized before the program can start. This can be problematic for large programs with many objects.