# Conceptual Overhead

- Similar to cyclomatic complexity
- Python famously holds as a value “Explicit is better than implicit”. This is not something Rubyists (or many functional programmers) value, instead favoring compactness or “elegance”
  - More compact the code, or the use of  language, library, and framework features (which are not well known) can exclude people from understanding or contributing
- verbosity vs complexity
- General coding concepts vs less popular coding concepts
- More complex domain vs less complex domain
  - this will always be a sticking point, and hard to split apart
  - yes can look at parts of the domain (abstract them - methods, classes), but as a whole you need to combine the parts
    - but following the flow can be hard
  - Cannot remove it as it is part of the requirements
  - Thus having less complex code (syntax/language features/patterns etc) allows your brain to spend more time being able to comprehend the main complexity that the app exists for (the domain)
- Reducing conceptual Overhead  
  - Increases the number of people  who can understand the system. This, then, increases the number of people who can make changes to the system
- elegance, beauty, compactness (and any other subjective measure) can be the bane of simplicity
  - stop writing professional code with this in mind
- Acid test:
  - When doing some work, need to decide if it is worth adding some pattern, principle, language feature, library, framework etc, if it
    - Makes the code readable, the allows you to focus on the domain
    - Makes it easy to add domain features
    - Makes it easy to change or fix bugs
    - Makes it easy to find

## Links

- https://naildrivin5.com/blog/2018/02/02/explicit-code-is-inclusive.html
- https://naildrivin5.com/blog/2019/06/29/simple-expressions-only.html
