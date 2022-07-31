# Rate Limiting

## what

- a rate limiter is used to control the rate of traffic sent by a client or a service.
- If the API request count exceeds the threshold defined by therate limiter, all the excess calls are blocked
  - Generally returning status code 429

### Examples of rate limiting

- A user can write no more than 2 posts per second.
- You can create a maximum of 10 accounts per day from the same IP address.
- You can claim rewards no more than 5 times per week from the same device

## Benefits

- Prevent resource starvation caused by Denial of Service (DoS) attack
- Reduce cost. Limiting excess requests means fewer servers and allocating more
resources to high priority APIs.
- Prevent servers from being overloaded.
- Used to enforce pricing structure of service
  - ie free tier will have stricter rate limits, compared to paid tier
- Allow specific endpoints to not have a rate limit for example monitoring

## Downsides

- another hope, increases latency
- If get this wrong could lose business or damage reputation
  - Need to monitor, check stats, test, and improve
- system might be working fine, but in peaks of traffic, could turn away users
  - should be elastic, or config changed to meet demand
- It's a brute force approach to DoS attacks, does not distinguish unless knows about user (ie jwt, ip add whitelisted)
- dropping requests that need to be processed
  - instead of dropping can move these requests to a queue, and these can resent to the service and processed if with in the rate limit
    - or batched to be done at later time when traffic is less

## where

- server side
  - prefered, in control
  - Location
    - In app
    - api gateway
- Client side
  - not in control, can be bypassed with malicious requests

## Technologies

- Proxies can have this available
- Istio https://istio.io/latest/docs/tasks/policy-enforcement/rate-limit/
- nginx https://www.nginx.com/blog/rate-limiting-nginx/
- there is always trade off between using an on the shelf implementation or build your own

## Informing clients

- can use headers to inform the client that they are being rate limited, how many requests left in time unit, how to wait to retry etc
- example
  - X-Ratelimit-Remaining: The remaining number of allowed requests within the window.
  - X-Ratelimit-Limit: It indicates how many calls the client can make per time window.
  - X-Ratelimit-Retry-After: The number of seconds to wait until you can make a request again without being throttled.

## Algorithms

### Token bucket
### Leaking bucket
### Fixed window counter
### Sliding window log
### Sliding window counter
