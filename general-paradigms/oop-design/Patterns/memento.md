# Memento Pattern

## What

- a solution to implement undoable actions without revealing the details of its implementation.
- Implements undo and redo

## How

- by saving the state of an object at a given instant and restoring it if the actions performed since need to be undone.
- The Memento pattern delegates creating the state snapshots to the actual owner of that state, the originator object. Hence, instead of other objects trying to copy the editor’s state from the “outside,” the editor class itself can make the snapshot since it has full access to its own state.
- components
  - Originator
    - the object whose state needs to be saved
    - can produce snapshots of its own state, as well as restore its state from snapshots when needed.
  - Caretaker
    - the object triggering the save and restore of the state
    - knows not only “when” and “why” to capture the originator’s state, but also when the state should be restored.
    - A caretaker can keep track of the originator’s history by storing a stack of mementos. When the originator has to travel back in history, the caretaker fetches the topmost memento from the stack and passes it to the originator’s restoration method.
  - Memento
    - is a value object that acts as a snapshot of the originator’s state. It’s a common practice to make the memento immutable and pass it the data only once, via the constructor.
  - the memento class is nested inside the originator. This lets the originator access the fields and methods of the memento, even though they’re declared private. On the other hand, the caretaker has very limited access to the memento’s fields and methods, which lets it store mementos in a stack but not tamper with their state.
    - In the absence of nested classes, you can restrict access to the memento’s fields by establishing a convention that caretakers can work with a memento only through an explicitly declared intermediary interface, which would only declare methods related to the memento’s metadata.
    - On the other hand, originators can work with a memento object directly, accessing fields and methods declared in the memento class. The downside of this approach is that you need to declare all members of the memento public.

## when

- used in situations where some actions are undoable, therefore requiring to rollback to a previous state.
  - However, if the state of the Originator is heavy, using the Memento Design Pattern can lead to an expensive creation process and increased use of memory.
  - Use event sourcing and databases
-  Use the Memento pattern when you want to produce snapshots of the object’s state to be able to restore a previous state of the object.
  -  The Memento pattern lets you make full copies of an object’s state, including private fields, and store them separately from the object. While most people remember this pattern thanks to the “undo” use case, it’s also indispensable when dealing with transactions (i.e., if you need to roll back an operation on error).
-  Use the pattern when direct access to the object’s fields/getters/setters violates its encapsulation.
  - The Memento makes the object itself responsible for creating a snapshot of its state. No other object can read the snapshot, making the original object’s state data safe and secure.

## Advantages

- can produce snapshots of the object’s state without violating its encapsulation.
- can simplify the originator’s code by letting the caretaker maintain the history of the originator’s state.

## Drawbacks

- The app might consume lots of RAM if clients create mementos too often.
- Caretakers should track the originator’s lifecycle to be able to destroy obsolete mementos.
-  Most dynamic programming languages, such as PHP, Python and JavaScript, can’t guarantee that the state within the memento stays untouched.

## Comparison with other patterns

- You can use Command and Memento together when implementing “undo”. In this case, commands are responsible for performing various operations over a target object, while mementos save the state of that object just before a command gets executed.
- You can use Memento along with Iterator to capture the current iteration state and roll it back if necessary.
- Sometimes Prototype can be a simpler alternative to Memento. This works if the object, the state of which you want to store in the history, is fairly straightforward and doesn’t have links to external resources, or the links are easy to re-establish.
