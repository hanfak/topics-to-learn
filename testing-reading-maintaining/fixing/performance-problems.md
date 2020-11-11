# How to Fix Performance Problems

- Performance of a system can easily be improved, with a little planning and experience/skills
  - But there is a asymptotic aspect of improving performance, you eventually get less bang (small % increase in performance metric) to the time spend doing so
  - Thus avoid major spending too much time optimising, unless it is required (SLA)
- Under time-to-market pressure, it is both wise and effective to choose a solution that gets the job done simply and quickly, but less efficiently than some other solution
  - performance is a part of usability, and often it must eventually be considered more carefully.
- Be aware when optimising, locally it might be slower on your machines compared to production
  - The benchmarks used or how they are collated might not be accurate
  - The compiler might do it's own optimisations after several repetitions
  - Just measuring, will influence the performance too

## How

- Need to analyse the system
  - Need metrics
  - Need evidence
  - Need to be able to replay this area of optimisation, to test your fix works
- Need to find the bottlenecks
  - places where most of the resources are consumed
  - No need to focus on optimising anything if it counts for a small % of computation time.
  - Focus on the big rocks first, the easy wins
- To do this, you will need tools, llike a profiler or other apps
  - logs will also help too
- Focus on things that will improve the system at least 2x for that metric
  - Or some big factor
- Any change that is made, will require testing, which needs to be factored in
  - Is the change to hard to test (or measure)?
- Well designed systems, especially if modular will contain the performance issue in the module (segratated section) and can just focus on that
  - May allow you to redesign that module instead, as better allocatio of time
- Might be the case, that all the easy wins do not help attian your performance goal
  - This can lead to doing the hard and time consuming stuff
  - It might be better to redesign system in this case
    - Less time to improve system and/or much better performance improvements

## Examples

- Using a database connection pool, instead of connecting to database everytime per call
- Using indexes in databases for common column looks up
- Using caching for non changing data (or hardly changing data)
- unnecessary I/O in inner loops
- leaving in debugging statements that are no longer needed
- Too many logs
- unnecessary memory allocation
- inexpert use of libraries
