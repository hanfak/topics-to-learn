# Clean Code

- This a controversial topic. As is opinionated and no set standard.
  - Depends on the cirucmstances of the code
    - Type of codebase
    - Industry
    - current practices
    - etc
- This should be enforced from a teams/department perspective for short and long term needs, defined and refined by the most experienced and respected developers.
  - And part of code reviews, and pairing.
  - Used in static analysis tests
  - Shared via learnings, brown bags etc
  - Part of assessment for promotions
  - Should have must do and could do parts
- Probably never achieve

## Clean code - Bob Martin

- A book of high repute, espousing many opinionated standards for writing clean code
- Giving to many new junior devs
  - Good standards to start off with, but must make sure they fit in with the current clean code patterns already in use
  - Eventually, deciding its trade offs and when to or not use 
- A people take it as gospal, rather than using it as ideas with trade offs
  - This happens due to the popularity of the author rather than content
- clean code can be different for different codebases, different companies etc

### Counter

- https://qntm.org/clean

## Issues 

- In my work I don't care about nanoseconds. I almost never care about microseconds. I sometimes care about milliseconds. Therefore I make the software engineering tradeoff towards programmer convenience, and long term readability and maintainability. This means that I don't want to think about the hardware. I don't want to know about Ln caches, or pipelining, or SIMD, or even how many cores there are in my processor. I want all that abstracted away from me, and I am willing to spend billions of computer cycles to attain that abstraction and separation. My concern is programmer cycles not machine cycles.
- I have, in the past, worn the other shoes. There was a time in my career when microseconds had to be conserved, when I had to meet submillisecond deadlines, and I counted and conserved cycles as carefully as Ebenzer Scrooge. So I think I understand your concern fairly well.
- clean code will be trading computer cycles for programmer cycles. And that's a good thing in most of the software teams and organizations
- https://youtu.be/DsAclZbP_Us  Abstraction Bad? | Clean Code : Horrible Performance : (Clip) Interview
  - Make code clean too fast or too early can be issue, this is predictive abstraction, and we cannot predict the future. 
    - unless we know the future requirements that will be worked in or soon or later
  - It's better to write the simplest code, may not have all the patterns and solid etc, but it works, and when it needs to be changed then do it at that time
    - ie 3 times then abstract

## Links

- https://www.youtube.com/watch?v=_Zqhs1IhGx4&t=1s
  - http://www.jeremybytes.com/Demos.aspx#CC
- https://betterprogramming.pub/clean-code-is-slow-but-you-still-need-it-anyway-ffcac6973c93
