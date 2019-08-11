# Transaction Script/ Use Case pattern

## What it is?
- Domain logic goes in here.
  - Single procedure for each action(http request) that a user might want to do
- Procedural in nature
- Takes input from presentation layer
  - validated or changed to be able to used here
- Flow of the process takes place
  - processes input with validations and calculations, stores data in the database, and invokes any operations from other systems
- Dependencies from outer layers are injected here using the interface
- The response is what is processed by the presentation layer
- avoid calls to presentation layer
  - Should not interact again


## Advantages

- easy to follow, clear structure
- Easy to use several depenencies to perform actions
- useful for simple domain logic

## Disadvantages

- can grow in complexity, and become big
  - dont want to extract to much logic as it adds layer of indirection
- Duplication can occur between different transaction scripts

## Other

- Can use command pattern for this
