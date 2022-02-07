# Weakest type

- For inputs
  - Instead of conreate impl, use interfaces
  - instead of ArrayList, use List, or Collection (if dont care about ordering) or ITerable (if dont care about the size)
    - This gives the user more flexibility, can use method with ArrayList, LinkedList etc
    - Reduces need to add more convience methods for different methods
    - avoids overloading
- For return type
  - Does it matter the need for the concreteness of impl or sub class with extra properties/behaviour
- Make the type more abstract, allows for change in implementatoin of api, without breaking the user
  - more flexibility
- As the signature is a contract with the user.
  - if the contract says the return type is a collection, and the user is uses this as so, then they are breaking the contract, not the developer 
