# First class functions

-  an essential feature of functional language
-  Functions are described as first-class when they can be treated like any other value: that is to say,
  -  they can be dynamically assigned to a name or symbol at runtime
  -  they can be stored in data structures
  -  passed in via function arguments
  -  returned as function return values
-  Similar to how pointers work
-  Also called Lambdas
  -  lambdas are unnamed/annoymous functions
  -  The point of a lambda function is where you need a function in that place and only there; since it is not needed anywhere else you simply define it right there. It doesn’t need a name.
    -  If you did need to reuse it somewhere else then you would consider defining it as a named function and referencing it by name instead
-  As function/lambda is passed as a variable (or is function form)
  -  it is not called immediately
  -  it can be called/invoked by whoever it was passed to
-  First-class functions are also the means for achieving asynchronous I/O
  -  allows to make non-blocking function call
  -  you pass it a reference to a function for it to call you back on when it is done
