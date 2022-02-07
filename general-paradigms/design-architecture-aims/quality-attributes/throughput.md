# Throughput

- Amount of owrk done in time taken
-  the maximum capacity of a machine or system
  - in factories to calculate how much work an assembly line can do in an hour or a day, or some other unit of time measurement.
  - the amount of data that can be passed around in a unit of time
  - ie a 512 Mbps internet connection is a measure of throughput - 512 Mb (megabits) per second.
  - ie if a server receives 1 million requests per second, and can serve only 800,000 requests, then its throughput is 800,000 per second
- there is a bottleneck because the server cannot send out more than N bits a second, but the requests are more than that.  A bottleneck is therefore the constraint on a system.
  - A system is only as fast as its slowest bottleneck.
  -  increasing throughput anywhere other than the bottleneck may be a waste - you may want to just increase throughput at the lowest bottleneck first.
- You can increase throughput
  -  by buying more hardware (horizontal scaling)
  - increasing the capacity and performance of your existing hardware (vertical scaling)
  - a few other ways.
- Increasing throughput may sometimes be a short term solution,
  - so systems designer will think through the best ways to scale the throughput of a given system
    - including by splitting up requests (or any other form of "load"), and distributing them across other resources etc.
- The key point to remember is what throughput is, what a constraint or bottleneck is, and how it impacts a system
- https://youtu.be/HrfgslRY7Ak
