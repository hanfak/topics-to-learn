# Complexity

- Biggest enemy of shipping quality software
- The aim of software is to build essential complexity (it's purpose) while not letting the accidental and other complexities affect this

## Types of complexity

- Congnitive (see ...)
- essential
  - The complexity in what the system does
  - The business logic, it is the value of the system being created and used
  - IF not there then system is useless
  - The difficulty of the complexity is dependent on the problem being solved by the system
    - calculating trajectory of space craft is more dificult than converting the temperature to different types
- accidental
  - Everythign that is not essential complexity
  - the problems that we are forced to solve as a side of effect of doing something useful (ie business logic)
  - ie persistance of data, displaying things on screen, security etc
  - This is still important to address, if not solved than the solutions to the essential complexity will not be usable
    - But building system that only deals with this complexity but did not deal with essential complexity then it will be useless
  - Aim to minimise this complexity
- Incidental
  - most counter-productive type
  - non desirable
  - Example something that is simple, easy to use vs something that has lots of features but hard to use
    - ie subversion vs git
- API
- Deployment
- Infrastructure


## How to deal with it

- Accidental and essential complexity solutions should not be mixed, they should be separated. Essential logic of system shouldnt not know how it is getting data to work on. This is part of **separation of concerns**
- The ideas of low coupling and high cohesion, aims to reduce this

##  cyclomatic complexity

## Links

- https://dev.to/alexbunardzic/software-complexity-essential-accidental-and-incidental-3i4d#:~:text=In%20order%20to%20gain%20correct,essential%2C%20accidental%20and%20incidental%20complexity
- https://www.codiga.io/blog/software-complexity-guide/
