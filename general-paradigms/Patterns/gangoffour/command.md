# Command Pattern

## command Dispatcher

- implement a centralized mechanism for handling commands. 
- The pattern separates the responsibilities of command execution and command dispatching into separate classes.

### How 
- commands are represented as objects that contain all the necessary information to perform a specific action
- The command dispatcher receives the command object and routes it to the appropriate command handler based on its type. 
- The command handler then executes the command and returns the result.

### Benefits 
- Centralized control: 
  - The pattern provides a centralized control mechanism for handling commands, making it easier to manage and maintain the codebase.
- Decoupling of components: 
  - The pattern decouples the components responsible for command dispatching and command execution, which promotes better modularity and flexibility in the codebase.
- Extensibility: 
  - The pattern can be extended easily to handle new types of commands, as each command type can be associated with its own handler.


### Cons 

- Complexity:
  - The pattern can introduce additional complexity to the codebase, particularly as the number of command types and associated command handlers grows.
- Performance: 
  - The pattern can introduce additional overhead in the dispatching and execution of commands, particularly in scenarios where a large number of commands are being processed.
- Testing: 
  - Testing command handlers can be more challenging, as they are often tightly coupled to the underlying system components they interact with.
- Over-engineering:
  - There may be scenarios where the use of the pattern is not justified, and it can be over-engineering to implement a command dispatcher.