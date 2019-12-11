# DNS

## Creating new DNS for old systems

- Can have multiple DNS ie aliases for the same endpoint.
- If the application is not changing the entrypoint to cater for the new path, can use nginx/ingress to map the new dns and path to the application's entry point path
  - ie app.com/ -> /
  - ie app.com/ and blah.com/ -> /
  - ie app.com/direct -> /direct

## Links

- https://www.freecodecamp.org/news/what-is-dns-anyway/
