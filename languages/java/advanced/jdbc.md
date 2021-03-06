# JDBC

## Connecting to a database

## Database pooling


## Statements (prepapred, statements)

### Prepared STatement

- allows you to write a parameterized query
- PreparedStatement is a class in java.sql package and allows Java programmers to execute SQL queries by using the JDBC package
- Prepared Statement queries are pre-compiled on the database and their access plan will be reused to execute further queries which allow them to execute much quicker than normal queries generated by Statement object.
-
- Benefits of prepared statement:
  - prevents sql injections
    - all values passed in to it, will be escaped automatically
  - better performance
  - allows you to write a dynamic and parametric query.
    - it's like a template, where you can set the values using specific methods
    - Much faster than using string concat to construct the sql
  - More readable
- Limitation
  - doesn't allow multiple values for one placeholder (?) who makes it tricky to execute SQL query with IN clause
  -

### Links
- http://www.java67.com/2018/03/jdbc-difference-between.html

## Executing statements

## Getting/reading results

### Use of iterator pattern
### Storing in object

## try with resources to close connections

## Other

- java.sql.Date only has the date portion no time
  - need to be careful when using java.util.Date as it contains time and date

## Links

- https://self-learning-java-tutorial.blogspot.co.uk/2014/10/jdbc.html
- https://docs.oracle.com/javase/tutorial/jdbc/basics/index.html
- https://www.tutorialspoint.com/jdbc/index.htm
- https://www.javatpoint.com/java-jdbc
- https://www.journaldev.com/2681/jdbc-tutorial
- http://tutorials.jenkov.com/jdbc/index.html
