# Integration Operation Segregation Principle

- Functions shall either only contain logic or they shall only call other functions.
  - "Logic" is the part of code which creates the actual software behavior. It's the transformations, control structures, and I/O- or API-calls provided by third parties.
  - "other functions" are functions of the same codebase which are under your control and not deemed to be internal frameworks (which would move them into the realm of logic).

https://ralfwestphal.substack.com/p/integration-operation-segregation
