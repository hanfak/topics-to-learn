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
