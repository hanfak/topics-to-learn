# Performance Fallacy 

- When it is pointed out that a common software practice is bad for performance, counter arguments ensue stating that performance is not a concern 
- This can either lead to discussions on trade offs, or the idea of this
- But can also lead to no discussion and taken as the norm that it does not matter about performance
- In fact performance always matter, it needs to be discussed and understood for each application/system
  - it may be that you dont need to focus too much on it, but it is a factor and should be considered
- The opposite is also an issue, where you always focus on performance, but it is not needed ie overoptimising 
  - only do it when necessary, measure (or get stats) first, focus on bottle necks, if a quick win to boost performance do it

## What is performance 
- the amount of resource consumption a program uses to do its job.
  - CPU time, wall-clock time, battery life, network traffic, storage footprint 
  - all the metrics that do not change the correctness of a program,
  - but which affect how long a user waits for the program to complete, how much of their storage it occupies, how much of their battery life it uses, etc.

## excuses for no need to discuss 
- Excuses:
  - No need. 
    - There’s no reason to care about software performance because hardware is very fast, and compilers are very good. Whatever you do, it will always be fast enough. Even if you prefer the slowest languages, the slowest libraries, and the least performant architectural styles, the end result will still perform well because computers are just that fast.
- Too small. 
  - If there is a difference in performance between programming choices, it will always be too small to care about. Optimal code will only have 5 or 10% better performance at best, and we can always live with 10% more resource usage, whatever resource it happens to be.
- Not worth it. 
  - Sure, you could spend time improving the performance of a product. That improvement might even be substantial. But financially, it’s never worth it. It’s always better for the bottom line to ignore performance and focus on something else, like adding new features or creating new products.
- Niche. 
  - Performance only matters in small, isolated sectors of the software industry. If you don’t work on game engines or embedded systems, you don’t have to care about performance, because it doesn’t matter in your industry.
- Hostpot. 
  - Performance does matter, but the vast majority of programmers don’t need to know or care about it. The performance problems of a product will inevitably be concentrated in a few small hotspots, and performance experts can just fix those hotspots to make the software perform well on whatever metrics we need to improve.

