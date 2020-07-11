# Latency

- It is the measure of a duration
  - The duration for an action to complete something or produce a result.
  - ie for data to move from one place in the system to another
  - You may think of it as a lag
- most commonly understood latency is the "round trip" network request
  - how long does it take for your client to send a query to your server, and get a response back from the server.
- Low latency is for this action to take as little time as possible
  - Fast lookups means low latency.
  - So finding a value in an array of elements is slower (higher latency, because you need to iterate over each element in the array to find the one you want) than finding a value in a hash-table (lower latency, because you simply look up the data in "constant" time , by using the key. No iteration needed.).
  - reading from memory (low latency) is much faster than reading from a disk (high latency)
- latency is the inverse of speed.
  - You want higher speeds, and you want lower latency.
  - Speed (especially on network calls like via HTTP) is determined also by the distance.
  - ie trade offs:  you want to design a system to avoid pinging distant servers, but then storing things in memory may not be feasible for your system.
  - ie websites that show news articles may prefer uptime and availability over loading speed,
  - ie online multiplayer games may require availability and super low latency.

## Links

- https://www.infoworld.com/article/3235340/4-sources-of-latency-and-how-to-avoid-them.html
- https://tech.forter.com/9-5-low-latency-decision-as-a-service-design-patterns/
- https://stackoverflow.com/questions/1209803/low-latency-programming
- https://www.youtube.com/watch?v=BD9cRbxWQx8
- https://medium.com/adobetech/engineering-high-throughput-low-latency-machine-learning-services-7d45edac0271
- https://dzone.com/articles/low-latency-java-part-1
