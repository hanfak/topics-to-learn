# Reuse existing interfaces 

- Instead of creating a new interface, reuse one that already exists
  - especially those that are part of the language or common libraries 

## Benefits

- Reduce bloat
  - Having too many interfaces can make the code too hard to follow 
- Reduce cognitive load 
  - Existing interfaces mean the devs are already comfortable with them  

## Negatives 

- Interface is a contract for a specific usage, although abstract it might not be abstract enough for use in multiple places 
  - Just because an interface is available, and can be used, does not mean it should be used, think about what the interface is for 
- 

## Example 

- Strategy Pattern
  - Instead of new interface, use a Function<INPUT,OUTPUT> or Consumer<INPUT> 
    - Can have another interface but that extends theses
  - The implementors will just implement this interface, and override this method 
  - These interfaces are single method interfaces, and thus lambdas/method ref can be used