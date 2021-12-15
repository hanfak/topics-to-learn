# PL SQL

- Programming with SQL
- Generally using procedural paragdigm

## General

- To run a function
  - 'SELECT <name of function> FROM DUAL;'
- Format of function:
```SQL
CREATE OR REPLACE FUNCTION <nameOfFunction>( arg1 IN VARCHAR2, arg2 IN NUMBER )
    RETURN VARCHAR2
AS
  -- variables used in function
  var1 VARCHAR2(20 BYTE);
BEGIN
  -- function body, can use the arg and var, as well as loops, if etc
  -- Can access the tables and columns, use sql

END <nameOfFunction>;
```

## Debugging

- When working with plsql, it helps to run it in an ide like SQL developer, where you can run the script against data
  - This can be done via code which will call the script, and have tests written, but sometimes feedback can be slow
  - In SQL developer (or alt) can split apart sections, replace variables with actual data, add print statements, check if it works quickly 
