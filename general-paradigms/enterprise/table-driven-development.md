# Table Driven Development 

- A software development technique 
- mentioned in Code Complete
- uses tables to store data and logic
- tables can be stored in memory or read from files (for the data only)
- allows you to look up information in a table rather than using logic statements (if and case) to figure it out. Virtually anything you can select with logic statements, you can select with tables instead.
- This is different to 
  - logic based
    - if/else or case statements 
  - object based approach 
    - using types to decide the type of method to use
    - you'd typically use an abstract message object with a subclass for each message type
    - Each time the format of any message changed, you'd have to change the logic in the routine or class responsible for that message

## When 
- for tasks that involve making decisions based on a set of inputs and outputs. 
- For example, a table-driven program could be used to calculate the tax owed on a purchase, or to determine the appropriate course of action for a customer service representative based on the customer's issue
- As the logic chain becomes more complex, tables become increasingly attractive

## How 

- you have to address the question of how to look up entries in the table.
  - You can use some data to access a table directly
    - ie months of the year and days in those months
  - Other data is too awkward to be used to look up a table entry directly.
    - ie social security numbers
  - Different types of access 
    - direct
      - array look
    - indexed
      - hashtable look
    - stair step
      - When data is stored for a range of values 
        - ie 0-10%, 10%-20% etc
        - ie 1-5,6-10,11-20  etc
      - can store data in index using top level like 10%,20% etc, 
        - then have a keyLookupGenerator which takes the value and finds the key, to use in the index, but index keys must be ordered
        - ie for numbers, given input 5, use the keyset to find the closets number (ceil) and output this and then use it with the index ie index[key]
        - ie can also use a simple number check >= and < on the bounds 
- what you should store in the table
  - Can be data
  - an action
    - you can store a code that describes the action or,
    - you can store a reference to the routine that implements the action

## Advantages 
- make code more readable and maintainable.
  - Tables can make code more readable and maintainable by providing a clear and concise way to store data and logic.
- it can help to reduce the amount of code that needs to be written
- it can make it easier to test and debug code.

## Disadvantages 
- can be more time-consuming to create and maintain tables than to write traditional code
- tables can be difficult to read and understand if they are not well-organized
- tables can be inflexible if the data or logic changes frequently.
  - it may not be the best fit for scenarios where the logic is highly dynamic or complex
  - Complex conditions or interactions between inputs might be challenging to express in a tabular format, resulting in convoluted or cumbersome tables.
- Increased complexity: Tables can increase the complexity of a project by adding an additional layer of abstraction.
- Initial setup and overhead
  - Setting up the data tables and maintaining them can require additional effort and time compared to writing direct conditional logic.
  - Constructing and managing the tables might involve parsing and validating the input, handling edge cases, and ensuring data integrity. 
  - This upfront setup and ongoing maintenance can introduce overhead, especially for smaller, less complex systems.
- Reduced performance
  - Table-driven development can potentially impact performance compared to direct conditional logic. 
  - The process of looking up inputs in the data tables and retrieving the associated outputs or actions may introduce additional computational overhead, particularly for large tables or time-sensitive operations
- Debugging and error handling can be more challenging in table-driven development.
  - When issues occur, diagnosing problems within the data tables, identifying incorrect mappings or missing cases, and tracing the flow of inputs and outputs can be more complex compared to traditional conditional logic.