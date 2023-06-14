# Mutability 

- Mutability is a way of life in imperative programming
- It's not bad, but shared mutability is
- Shared mutability
  - is where a piece of code mutates variables or objects outside its immediate local scope.
  - We're so used to shared mutability that it may appear impossible to implement some logic without mutating variables

## Advantages 

- Performance efficiency
  - Mutable data structures can be more efficient in terms of time and memory usage when frequent modifications or updates are required. 
  - Instead of creating new copies of the entire data structure, mutable structures allow direct modifications to existing data, reducing the need for memory allocation and potentially improving performance.
- Simplicity and readability
  - Mutable data structures can be easier to work with and understand, especially for developers who are more accustomed to imperative programming paradigms. 
  - you can modify values directly, making the code more straightforward and readable in certain cases. 
- Compatibility with certain algorithms
  - Some algorithms are naturally designed to work with mutable data structures, particularly those that involve in-place modifications or rely on mutable state. 
  - Adapting such algorithms to work with immutable data structures can sometimes be complex or less efficient.
- Flexibility
  - Mutability allows for dynamic changes to data, making it easier to handle scenarios where frequent updates, additions, or deletions are necessary. 
  - Mutable data structures provide the flexibility to modify the data in response to changing requirements or real-time data updates.
- Interoperability with external libraries or APIs
  - Many existing libraries and APIs are designed to work with mutable data structures. 
  - If your codebase heavily relies on external dependencies that expect mutable data, using mutable structures can simplify integration and reduce the need for additional adaptation or conversion layers.
- Memory efficiency
  - In certain cases, mutable data structures can consume less memory compared to immutable counterparts. 
  - Since mutable structures can update values in place, they may avoid the need to duplicate data, resulting in lower memory overhead.
- Efficient data streaming
  - Mutable data structures are well-suited for scenarios where data is processed in a streaming fashion, and intermediate modifications are required before the final result is obtained.
  - Mutable structures enable incremental updates without the need to create and maintain multiple copies of the data.

## Disadvantages 

- suffers from primitive obsession
  - We have to deal with the low level - the how
- Creation of temp variables
  - ie the "i" in the for loop or "total" in summing values
  - Adds noise 
- The more mutability we have in code, the harder it is to reason the code. 
  - The more variables and state changes added the more complex it gets
  - make sure the states change correctly and in the right order.
- the higher the chances of bugs
  - Mutability introduces moving parts, and since they are hard to reason, it's easier to make mistakes with state transitions.
- Hard to parallelize the code.
  - Creating threads is not that hard, but we'll quickly run into thread safety issues due to the mutable variable. Shared mutability means lack of thread-safety.
  -  make this code thread-safe we have to put locks or synchronization primitives around the change to the mutable variable. This introduces accidental complexity in code, makes it harder to understand, and leads to more bugs as well