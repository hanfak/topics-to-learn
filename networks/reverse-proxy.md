# Reverse Proxy

- A server that sits in front of a web server, and forwards clients requests to the web server.
- a type of proxy server that typically sits behind the firewall in a private network and directs client requests to the appropriate backend server.
- Acts as a middleman
- when clients send requests to the origin server of a website, those requests are intercepted at the network edge by the reverse proxy server. The reverse proxy server will then send requests to and receive responses from the origin server
- ensures that no client ever communicates directly with that origin server.
- Why?
  -  ensure the smooth flow of network traffic between clients and servers.
  - Load balancing
    - A popular website that gets millions of users every day may not be able to handle all of its incoming site traffic with a single origin server. Instead, the site can be distributed among a pool of different servers, all handling requests for the same site.
    - a reverse proxy can provide a load balancing solution which will distribute the incoming traffic evenly among the different servers to prevent any single server from becoming overloaded. In the event that a server fails completely, other servers can step up to handle the traffic
  - Protection from attacks
    - a web site or service never needs to reveal the IP address of their origin server(s). This makes it much harder for attackers to leverage a targeted attack against them, such as a DDoS attack.
    - Instead the attackers will only be able to target the reverse proxy, which will have tighter security and more resources to fend off a cyber attack.
  - Global Server Load Balancing
    - website/apps can be distributed on servers across the world. the reverse proxy will send clients to the server that’s geographically closest to them. This decreases the distances that requests and responses need to travel, minimizing load times.
  - Caching
    - A reverse proxy can also cache content, resulting in faster performance.
    - if a user in Paris visits a reverse-proxied website with web servers in Los Angeles, the user might actually connect to a local reverse proxy server in Paris, which will then have to communicate with an origin server in L.A. The proxy server can then cache (or temporarily save) the response data. Subsequent Parisian users who browse the site will then get the locally cached version from the Parisian reverse proxy server, resulting in much faster performance.
  - SSL encryption
    -  Encrypting and decrypting SSL (or TLS) communications for each client can be computationally expensive for an origin server. A reverse proxy can be configured to decrypt all incoming requests and encrypt all outgoing responses, freeing up valuable resources on the origin server
    - Useful for apps in a kubernetes cluster, which have many apps communicating via http. The internal apps can then just communicate via http instead of https.
  - Web acceleration
    -  Reverse proxies can compress inbound and outbound data
  - ensures that multiple servers can be accessed from a single record locator or URL regardless of the structure of your local area network.



# Foward proxy

-  is a server that sits in front of a group of client machines, and forwards clients requests to the web server.
- often called a proxy, proxy server, or web proxy
- ensures that no origin server ever communicates directly with that specific client.
- Why
  - To avoid state or institutional browsing restrictions (ie firewalls)
    - A forward proxy can be used to get around these restrictions, as they let the user connect to the proxy rather than directly to the sites they are visiting.
  - To block access to certain content
    - a school network might be configured to connect to the web through a proxy which enables content filtering rules, refusing to forward responses from Facebook and other social media sites.
  - Hide IP address
    - Only the IP address of the proxy server will be visible.
- Similar to a VPN
