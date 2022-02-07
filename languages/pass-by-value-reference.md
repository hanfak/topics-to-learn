# Pass by value vs Pass by reference

- Java is pass by value   
  - But objects are assigned to variables by their reference
  - primitives use their values
## What is Pass by value

## What is Pass by reference

## Benefits of pass by reference

- There is no copy of the argument made, hence, it is fast.
- To avoid changes done unintentionally we can even make it pass by const reference.
- We can return multiple values from a function.
- Since arguments are not copied into the new variables, it provides greater time and space efficiency
- Runtime polymorphism can be achieved
- Reduction of Memory
  - With passing it as value, function copies 1GB of data that’s passed to it. In total, your program consumes 2 Giga bytes of memory.
  - With passing it as a reference, function instead of copying the data directly access the existing data 1GB. The data alteration by function can be secured by applying “const” to the reference parameter in the function.

## Disadvantages of pass by reference

- As using a reference, you can alter the underlying object state (if the object is mutatble, ie List)
-

## Benefits of pass by value
## Disadvantages of pass by value 
