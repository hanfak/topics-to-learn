# Avoid returning nulls

This can lead to possible NPE

Instead:
  - return null object
  - enum that covers all cases
  - a default in a switch/case
  - empty List
  - optional
