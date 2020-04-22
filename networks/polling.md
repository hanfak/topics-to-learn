# Polling

- Used To have data in your application updated regularly or instantly

## What

- having your client "check" send a network request to your server and asking for updated data.
- These requests are typically made at regular intervals like 5 seconds, 15 seconds, 1 minute or any other interval required by your use case.

## When

-  polling is best used in circumstances when small gaps in data updates is not a problem for your application.
- For example, if you built an Uber clone, you may have the driver-side app send driver location data every 5 seconds, and your rider-side app poll for the driver's location every 5 seconds.
- if it's OK to have a lag (as little as 15 seconds is still a lag) then polling may be a good option

## Drawbacks

- Polling every few seconds is still not quite the same as real-time
- For large number of users
  - almost-constant network requests (not great for the client)
  - almost constant inbound requests (not great for the server loads - 1 million+ requests per second!)
- polling rapidly is not really efficient or performant, and polling is best used in circumstances when small gaps in data updates is not a problem for your application.
