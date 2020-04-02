# DNS


## What

- DNS stands for “Domain Name System”
- At the most basic level DNS provides a key/value lookup from a domain name (e.g., google.com) to an IP address (e.g., 85.129.83.120), which is required in order for your computer to route a request to the appropriate server.
  - Analogizing to phone numbers, the difference between a domain name and IP address is the difference between “call John Doe” and “call 201-867–5309.”
-  you need DNS to look up the IP address for a domain
- 


## Creating new DNS for old systems

- Can have multiple DNS ie aliases for the same endpoint.
- If the application is not changing the entrypoint to cater for the new path, can use nginx/ingress to map the new dns and path to the application's entry point path
  - ie app.com/ -> /
  - ie app.com/ and blah.com/ -> /
  - ie app.com/direct -> /direct

## Links

- https://www.freecodecamp.org/news/what-is-dns-anyway/
