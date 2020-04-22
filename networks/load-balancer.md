# Load balancer

## What

- They’re the magic sauce that makes scaling horizontally possible. They route incoming requests to one of many application servers that are typically clones / mirror images of each other and send the response from the app server back to the client.
  - Any one of them should process the request the same way so it’s just a matter of distributing the requests across the set of servers so none of them are overloaded.
- Problem: When a server simultaneously receives a lot of requests, it can slow down (throughput reduces, latency rises).  After a point it may even fail (no availability).
  - Solution: You can give the server more muscle power (vertical scaling) or you can add more servers (horizontal scaling).
    - With horizontal scaling, you got to work out how the income requests get distributed to the various servers - which requests get routed to which servers and how to ensure they don't get overloaded too?
    - In other words, how do you balance and allocate the request load?
- load balancers are like traffic managers who direct traffic.
- load balancers can be thought of as reverse proxies

## How

- A load balancer's job is to sit between the client and server (but there are other places it can be inserted) and work out how to distribute incoming request loads across multiple servers, so that the end user (client's) experience is consistently fast, smooth and reliable.

## Why

- Used to maintain availability and throughput.

## Server Selection Strategies

- How it decides how to route and allocate request traffic
- every time you add a server, you need to let your load balancer know that there is one more candidate for it to route traffic to.
- If you remove a server, the load balancer needs to know that too.
- The load balanacer configuration ensures that the load balancer knows how many servers it has in its go-to list and which ones are available.
- the load balancer can be kept informed on each server's load levels, status, availability, current task and so on.
- Approaches
  - A naive approach to this is for the load balancer to just randomly pick a server and direct each incoming request that way.
    -  randomness can cause problems and "unbalanced" allocations where some servers get more loaded than others, and that could affect performance of the overall system negatively.
  - Round Robin and Weighted Round Robin
    - How we process lists that loop
      - you start at the first item in the list, move down in sequence, and when you're done with the last item you loop back up to the top and start working down the list again.
    - load is pretty evenly distributed across your servers in a simple-to-understand and predictable pattern.
    - Adding weights to the server
      - Causes preferences to some servers over others
      -  the total traffic will be split up in proportion to those weights and allocated accordingly to the servers that have power proportionate to the volume of requests.
  - Load-based server selection
    - work out the current capacity, performance, and loads of the servers in their go-to list and allocate dynamically according to current loads and calculations as to which will have the highest throughput, lowest latency etc.
    - by monitoring the performance of each server and deciding which ones can and cannot handle the new requests.
  - IP Hashing based selection
    - to hash the IP address of incoming requests, and use the hash value to determine which server to direct the request too
    - ie  If I had 5 servers available, then the hash function would be designed to return one of five hash values, so one of the servers definitely gets nominated to process the request.
    - useful where you want requests from a certain country or region to get data from a server that is best suited to address the needs from within that region,
    - where your servers cache requests so that they can be processed fast.
      - you want to ensure that the request goes to a server that has previously cached the same request, as this will improve speed and performance in processing and responding to that request.
      - If your servers each maintain independent caches and your load balancer does not consistently send identical requests to the same server, you will end up with servers re-doing work that has already been done in as previous request to another server, and you lose the optimization that goes with caching data.
  - Path or Service based selection
    - to route requests based on their "path" or function or service that is being provided.
    - ie if you're buying flowers from an online florist, requests to load the "Bouquets on Special" may be sent to one server and credit card payments may be sent to another server.
      - If only one in twenty visitors actually bought flowers, then you could have a smaller server processing the payments and a bigger one handling all the browsing traffic.

## Consistent hashing

- https://www.cs.cmu.edu/~adamchik/15-121/lectures/Hashing/hashing.html
  -  is that hashing converts an input into a fixed-size value, often an integer value (the hash).
- One of the key principles for a good hashing algorithm or function is that the function must be deterministic, which is a fancy way for saying that identical inputs will generate identical outputs when passed into the function.
- Sometimes the hashing function can generate the same hash for more than one input - this is not the end of the world and there are ways to deal with it
  - when more than one input deterministically generates the same output, it's called a "collision".
- Example
  - Let's say you have 5 servers to allocate loads across.  An easy to understand method would be to hash incoming requests (maybe by IP address, or some client detail), and then generate hashes for each request.  Then you apply the modulo operator to that hash, where the right operand is the number of servers.
```
request#1 => hashes to 34
request#2 => hashes to 23
request#3 => hashes to 30
request#4 => hashes to 14

// You have 5 servers => [Server A, Server B ,Server C ,Server D ,Server E]

// so modulo 5 for each request...

request#1 => hashes to 34 => 34 % 5 = 4 => send this request to servers[4] => Server E

request#2 => hashes to 23 => 23 % 5 = 3 => send this request to servers[3] => Server D

request#3 => hashes to 30 => 30 % 5 = 0 => send this request to  servers[0] => Server A

request#4 => hashes to 14 => 14 % 5 = 4 => send this request to servers[4] => Server E
```

- Adding Servers, and Handling Failing Servers
  - Issues
    - we could add a sixth server but that would never get any traffic because our mod operator is 5, and it will never yield a number that would include the newly added 6th server.
    - he hashing function (refer to the pseudo code snippet above) still thinks there are 5 servers, and the mod operator generates a range from 0-4.  But we only have 4 servers now that one has failed, and we are still sending it traffic.
  - Solution consistent hashing
    - Consistent hashing does not eliminate the problems, especially adding new servers. But it does reduce the problems a lot. the underlying downside still exists - yes, but to a much smaller extent, and that itself is a valuable improvement in very large scale systems.
    - Consistent hashing applies a hash function to incoming requests and the servers. The resulting outputs therefore fall in a set range (continuum) of values.  This detail is very important.
    - https://www.youtube.com/watch?v=tHEyzVbl4bg

## Links

- https://blog.containership.io/7-things-that-nobody-told-you-about-load-balancers-that-you-ought-to-know

##  Nginix & Proxy servers

- https://nginx.org/en/
- https://www.nginx.com/resources/wiki/
- https://en.wikipedia.org/wiki/Nginx
- https://en.wikipedia.org/wiki/Proxy_server
