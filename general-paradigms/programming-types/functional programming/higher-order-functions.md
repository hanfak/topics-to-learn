# Higher Order Functions

- Definition
  - when a function accepts another function as its argument, or it yields another function as its return value
  - or both
- Examples
  - map, filter

## Function composition

- To compose two functions means to arrange them so that the result of one function is applied directly as the input of the other function.
- it is useful to consider two composed functions as a third function in its own right.
- It is a form of chaining
- Say you have a function f that takes a value x as its argument and returns a value y :
  - f ( x ) = y
  - and you have another function g that takes y as its argument and returns z
  - g ( y ) = z
  - clearly, then, you can apply g to the output of f like this :
  - g ( f ( x )) = z
  - This implies, therefore, that there is a third function h that maps x directly to z :
  - h ( x ) = z
- Examples
  - unix pipes ie `ls -al | grep blah`
  - map(x -> ...).filter(x -> ...)
  - builder pattern
