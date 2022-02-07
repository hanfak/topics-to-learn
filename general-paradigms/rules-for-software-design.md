# Rules for software designs

- These can be contentious, every one has their own set, and some have a following (sometimes cultist)
- There are not one set to rule them all, each have trade offs, some might work well in some domain but not in others
  - Nothing is perfect
- this is just a list of some of the general rules

## Kent Beck

The list:
- Runs all the tests
- Has no duplicated logic. Be wary of hidden duplication like parallel class hierarchies
- States every intention important to the programmer
- Has the fewest possible classes and methods

https://martinfowler.com/bliki/BeckDesignRules.html

## Copeland

The list:
- is well-covered by passing tests.
- has no abstractions not directly needed by the program.
- has unambiguous behavior.
  -  the less ambiguous the code’s behavior is, the better chance we have of successfully changing it
  - this might mean writing more code or being more explicit, or even duplicating things here and there
- requires the fewest number of concepts
  - To understand what code will actually do, we need to understand not only the domain, but also all of the concepts involved in that code
  - the more concepts exist in a design, the harder that design will be to understand.


https://naildrivin5.com/blog/2019/07/25/four-better-rules-for-software-design.html

- Design is About Balancing Cohesion and Coupling
  - Not blindly following principles

## Get shit done (lean/agile)

faster, better, cheaper than anyone.

1. Develop for today ( You are not gonna need it - YANGNI )
  1. Do not forget tomorrow ( Do not Repeat Yourself )
  2. Totally ignore days after tomorrow ( things change every month )
2. Fastest finger first wins
  1. When the quality is high enough ( happy customer )
  2. Tomorrow is taken care of ( build for immediate future )
3. Smallest Code wins
  1. Given Tomorrow people would be able to understand it - ( Principle of Least
Astonishment )
  2. Code is provably correct ( CHC )
4. Developers gets judged on:
  1. Less experience - how fast code and how much with quality
  2. Higher experience - how much code they removed from existing source code base
5. Only measure of code compaction is - Kolmogorov complexity
6. Code complexity measures like Cyclomatic are dangerously modular ( Assembly Line
Complexity )

in a product company, any product company, really, no one cares about the lines of code
that have been written

## Others

- https://www.ics.uci.edu/~emilyo/SimSE/se_rules.html
- https://www.geeksforgeeks.org/20-golden-rules-to-learn-in-software-development/
