# Guard Clause

- A coding technique
-  known as Early Return or Bouncer Pattern

## Uses 

- A `if-else` block has return statements can convert to a single guard clause 
  ```java
  if (x < 1) {
    return "Not a natural number";
  } else {
    return " a natural number";
  }
  ```
  To 
  ```java
  if (x < 1) {
    return "Not a natural number";
  }
  return " a natural number";
  ```
  - Can be used validation for inputs
     - consisting in an early exit of a function based on preconditions check.
      ```java 
      if (isNull(x)) {
          throw new IllegalArguementException();
      }
      ```
    - If no return in if statement, can use a blank return:
    ```java 
    void describeEating(Item item) {
      if (!item.isFood) {
        print("Wait, that's not even food!");
      } else {
        if (item.isDelicious) {
          print("Hmm, that was good.");
        } else {
          print("Not bad. Nutritious.");
        }
      }
     }
    ```
    to 
    ```java
    void describeEating(Item item) {
      if (!item.isFood) {
        print("Wait, that's not even food!");
        return;
      }

      if (item.isDelicious) {
         print("Hmm, that was good.");
      } else {
          print("Not bad. Nutritious.");
      }
    }
    ```

## Benefits

- makes code more readable
  - reduces indentation of your code and therefore makes your code much easier to read and reason about.
  - reduce size of if statements
- it allows exceptions handling to be placed at the beginning
  - to fail fast 
- It improves code, like performance 
  - by not exiting early, parts of code does not have to be run (ie http/database calls )

## Issues 

- Overuse 
  - especially with validating arguments for every method.
  - Should only do at edge (api) of code, to reduce polluting codebase

## Links 

- https://careers.per-angusta.com/blog/common-mistakes-with-guard-clause-pattern/