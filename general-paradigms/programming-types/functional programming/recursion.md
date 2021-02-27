# Recursion

- https://www.freecodecamp.org/news/how-recursion-works-explained-with-flowcharts-and-a-video-de61f40cb7f9/

- To avoid mutating stating, using recursion is method of doing so
- functional programming, and languages leads you to use this way of coding instead of using  loops
  - Some languages have been built to perform well with recursion
- To use, must have some idea beforehand how deep the recursion will go, lest you blow the stack.


## How it works

- A program that jumps to a subroutine pushes the return address on the stack, to be popped when the subroutine completes. If that subroutine calls another subroutine, then it pushes its own return address on top. The stack holds all the return addresses in the correct order so that the program is always able to return control back to where it came from
- Obviously, the greater the depth of nesting in your subroutines, the more stack space is required


## Avoiding blowing stack

- The key is to position the subroutine calls so that they are in tail position
  - This means that there are no more instructions between the return of control from the subroutine, and the end of the routine that called it.
  - ie when subroutine A calls subroutine B from tail position, control returns from B only to return immediately to the caller of A
- Example of not using tail poistion is factorial impl
  - The recursive call to factorial is not in tail position, because its result must be multiplied with n to calculate the return value for the outer function call
- why does this work
  - a subroutine call in tail position can be replaced with a goto. Unlike a subroutine call, a goto does not anticipate control returning to the calling routine, so no return address is pushed on the call stack.
  - Example
    - a -> b -> c
    - if the call to C is in tail position then B may as well go to C directly, leaving its own return address on top of the call stack, because C will pop that address and return directly to A. This is what we wanted to happen anyway. This is called tail call elimination and the benefit is twofold: firstly, we’ve avoided one unnecessary jump instruction, and much more importantly, we’ve avoided growing the call stack.
  - If you eliminate tail calls this way in a recursive algorithm, you get a routine that repeatedly jumps to its entry point until the terminating condition is achieved. In machine terms this is no different to a regular loop!
    - But this is programming language specific opitmisation
    
## Disadvantages of recursion

- Issues with stackoverflow errors
  - Java has no Tail Call optimization (yet), hence yes, recursive solutions may give you StackOverflowError.
- performance loss as it has to create new stack frame and do some other stuff for each recursive invocation.
- Readability might be harder
- Harder to debug
- using recursion can also restrict you from using concurrency to speed up parallel operations.
- Not as performant as loops
- https://stackoverflow.com/questions/41469031/is-recursion-a-bad-practice-in-general
-
