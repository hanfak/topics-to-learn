### Accessors and variable scope

- variable scope is where the variable is accesible
- parameters and variables declared in method are only avialable in that method.
  - when method ends, the reference of the variable goes away and cannot be accessed again
- instance fields are avialable in any instance method in the class
  - accessors does not affect this
  - stays in scope until the object is deleted (garbage collector)
- static variables are avialable
  - only defined in class not method
  - shared among all instances of any class.
  - not thread safe, must be made final
  - stays in scope until program ends
- loop scope
  - where a variable is declared in the loop ie for loop, and is thus only accessed in the loop.
- block scope
  - variable declared in block, ie if block, can only be used in that block, when block finishes it is destroyed.

- This
  - Example:
    ```java
    private String username;

    public void changeUsername(String newName) {
      this.username = newName;
    }
    ```
  - Conflicting local variable and class variable has the same name.
  - this prevents conflicts
  - this refers to the class variable


### Public

### Package protected (default)

### protected

### private

### Links
