# Conditonal/Flow control

<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Conditonal/Flow control](#conditonalflow-control)
	- [Links](#links)
	- [if](#if)
	- [Nested if](#nested-if)
	- [Ternary](#ternary)
	- [Case/Switch](#caseswitch)

<!-- /TOC -->

- Changing the flow of instructions
- ```Switch/Case```
  - follow through if no `break` at the end of the block
  - `default`
    - when all cases have not been matched, it run block in this section
  - In case statement, they can only be compile time constants of same data type of switch value ie
    - literals
    - enum constants
    - final constant variables which has been initialized
  - Multiple cases
    ```java
    case 'A':
    case 'B':
    case 'C':
        doSomething();
        break;

    case 'D':
    case 'E':
        doSomethingElse();
        break;
    default:
      doDefaultStuff();
      break;
    ```
    - Cases, A,B,C will all doSomething() then escape (break out of switch statement)
    - Cases D,E will all doSomethingElse() then break out.
- ```Break```
  - will exit out of the loop/case when hit
- ```if/else```
- ```else if```
- ```return```
- Use of block ```{}```
  - Dont need them if only one line statement
  - good to have
- Nested if statements
  - Avoid hard to read
  - if needing to write a flow chart, needs to be refactored
- ternary operator
  - Only for simple cases, can be hard to read

## Links

## if

- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/if.html
- https://www.tutorialspoint.com/java/if_else_statement_in_java.htm

## Nested if

- https://www.tutorialspoint.com/java/nested_if_statements_in_java.htm
- https://howtoprogramwithjava.com/nested-if-statements/

## Ternary

- http://www.cafeaulait.org/course/week2/43.html
- https://alvinalexander.com/java/edu/pj/pj010018

## Case/Switch

- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/switch.html
- https://www.tutorialspoint.com/java/switch_statement_in_java.htm
- https://blog.codefx.org/java/switch-expressions/
