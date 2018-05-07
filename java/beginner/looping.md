# Looping/Iterating
- Repeating the same task
- Doing the same thing across a data structure
- ```for```/```while```/```do while``` (imperative)

## While

- Format

```java
while(booleanExpression) {
  //body
}
```
- need to ensure that loop is terminated
  - what the booleanExpression is for
  - Can make booleanExpression = true, and loop will be infinite
    - but have a `break` in the body to exit the loop

## Do While

- Format
```java
do {
  //body
} while(booleanExpression)
```
- similar to while loop, but always does one execution of the body first.

## For

### Old/basic

- Format
```java
for(initialization; booleanExpression; updateStatement) {
  //body
}
```
- Not good for functional style as initialization has mutated variable.
- initialization can declared in the loop, and has scope just for the for loop.
  - Can declared outside of loop, initialized in loop and thus have scope inside nad outside of loop
  - If declared and init outside of loop, but reinit inside for loop, error will occur
- Inifinite loop `for(;;) { // body }`
- All components in for loop are optional
- Can have multiple initialization statements, booleanExpressions and updateStatements
  - Must have same data type in initialization

### New/enhanced

- aka for-each loop
-format
```java
for (datatype instance : collection) {
  //body...
}
```
- `collection` must implement Iterable interface
- 

## break statement

-  using a label (which is optional)
```java
aLabel: while (x > 5) {
  // some logic
  while (x.isEven) {
    // some logic
    break aLabel;
  }
}
```
  - This will break out of the top level loop instead of inner loop where the break is set.
- used in while/do while/switch/ for

## continue statement

- finishes the flow of the current loop.
- Uses the same syntaz as that of break when using optional lables
- used in while/do while/for

## Recursion

- stackoverflow exception

## Nested loops

#### Links

## for
- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html
- https://www.javatpoint.com/java-for-loop
- https://www.tutorialspoint.com/java/java_for_loop.htm


## while
- https://www.javatpoint.com/java-while-loop
- https://docs.oracle.com/javase/tutorial/java/nutsandbolts/while.html
- https://www.tutorialspoint.com/java/java_while_loop.htm

## do while
- https://www.javatpoint.com/java-do-while-loop
- https://www.tutorialspoint.com/java/java_do_while_loop.htm

## break, continue
- https://www.javatpoint.com/java-break
- https://www.javatpoint.com/java-continue

## Nested loops
- https://www.programiz.com/java-programming/nested-loop

## other
- https://stackoverflow.com/questions/8880870/java-for-vs-whiletrue
-
