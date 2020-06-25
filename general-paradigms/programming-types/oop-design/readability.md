# Readability

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Readability](#readability)
	- [Naming booleans](#naming-booleans)
	- [Method length](#method-length)
	- [Remove Unused Code](#remove-unused-code)
	- [Nesting](#nesting)
	- [Naming Variables and Parameters](#naming-variables-and-parameters)

<!-- /TOC -->

- Code is written for humans not compilers
  - compiler does not have to maintain the code over time - humans do.
  - Code needs to be easily understood for it to be soft


- Qualities of readable code
  -  Makes crystal clear the programmer’s intent
  - Makes it easy for bugs to stand out
  - Can be easily understood and changed by other programmers
  - Creates fewer surprises and annoyances when being read

- Reduces the mental effort required to understand it and therefore be able to change it safely.


## Naming booleans

 - The readability of logical constructs such as an if statement can often be improved by the introduction of a well-named, intermediary variable

 ```java

 if(ageInYears==40 && isEyeColorBlue && firstName=="Julia") {
    // etc.
 }

boolean isValid=ageInYears==40 && isEyeColorBlue && firstName=="Julia";
if(isValid) {}
// etc.
}
 ```

- If the code is performing some action when something is invalid, it can make sense to rename the isXXX to isNotXXX so that the reader doesn’t have to think as much
  - ie use isNotValidPerson rather than !isValidPerson

## Method length

- Methods with lots of lines of code tend to be harder to understand than methods with fewer lines of code.
- Can set a number of lines but treat it as a guide, with the full knowledge that as the number of lines increases, readability decreases.
- Some methods will be very long, ie applying business logic in usecase. But accept this to keep all logic in one place


## Remove Unused Code

- Every line of code that needs to be read has a mental cost associated with it.
- IDE should help with this
- This includes commented out code
- Can always use source control to go back to it

## Nesting

- Multiple levels of nested code (ifs, loops, etc.) can reduce readability.
- Can use guard clauses, or extract method to reduce nesting

## Naming Variables and Parameters
