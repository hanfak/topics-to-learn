# Avoid Checked Exceptions

- They dont work well with the use of lambdas, more verbose
- What people do with checked Exceptions, 
  - Log it
  - printstack
  - empty block
  - throw unchecked exception
  - sout
- Best thing to do is wrap in unchecked exception,
  - Handle it in better return type or propagate to user
