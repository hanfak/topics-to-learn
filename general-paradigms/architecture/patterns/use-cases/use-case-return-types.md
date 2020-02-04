# Use case return types

Use case/ application classes within a clean architecture, or any class which handles the business logic and interaction with outgoing infrastructure services (ie database, api calls), must return something for incoming infrastructure/adapter to process and return to user of app.

Issues with complex business logic is we return multiple responses, generally
- happy path
- sad path
- exception

Some patterns, just return the happy path (some type or void) and the sad path is a specific business exception, which gets caught at the web adapter layer and rendered there, with all other exceptions being caught by an error handler which gives a generic response.  Problem with this, is that we are using exceptions to drive logic, which is similar to the problems with using 'goto' in procedural languages. We would like to have exceptions thrown for exceptional things ie database connections fail, and then log it along with the stack trace.

## Ways of return multiple types

- As an array
  - Will need an interface
- As a tuple
- As a map
- Using railway programming
  - see Business flows library
- Create a wrapper object of all possible return types
  - This will lead to null values
  - Can get away with this by making all fields an array, and if not populated create new empty list
    - Alternatively use optional, but having optionals as fields is contentious so need to discuss
