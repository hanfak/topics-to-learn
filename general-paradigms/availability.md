# System Availability

- Software engineers aim to build systems that are reliable.  A reliable system is one that consistently satisfies a user's needs, whenever that user seeks to have that need satisfied.
  - A key component of that reliability is availability
- the **resiliency** of a system
  - If a system is robust enough to handle failures in the network, database, servers etc, then it can generally be considered to be a **fault-tolerant** system - which makes it an available system.
- Availability is only as strong as it's weakest link, so all systems that are used should also be available

## Quantifying Availability

- we calculate the percentage of time that the system's primary functionality and operations are available (the uptime) in a given window of time.
- most business-critical systems would need to have a near-perfect availability.
- Systems that support highly variable demands and loads with sharp peaks and troughs may be able to get away with slightly lower availability during off-peak times.
- all depends on the use and nature of the system.
-  in general, even things that have low, but consistent demands or an implied guarantee that the system is "on-demand" would need to have high availability.
- Example
  - Think of a site where you backup your pictures.  You don't always need to access and retrieve data from this - it's mainly for you to store things in.  You would still expect it to always be available any time you login to download even just a single picture.
  - in the context of the massive e-commerce shopping days like Black Friday or Cyber Monday sales.  On these particular days demand will skyrocket and millions will try to access the deals simultaneously.  That would require an extremely reliable and high-availability system design to support those loads.
- uptimes are calculated based on the full day (all 24 hours) so a downtime of "just 5%" will mean 1.2 hours a day.  Which is 36 hours a month.  That's a lot, because that could happen continuously -  1.5 consecutive days.  Not acceptable!
  - Think five 9s. Uptime of 99.999%
  - In the case of 99.99% uptime, that's 4 nines. That sounds good, but over a year thats more than 3.5 days down.
  -  "five nines" is considered the ideal availability standard because that translates to a little over 5 minutes of downtime per year.

## Why Have it

- A commercial reason for high availability is simply that any downtime on the site will result in the site losing money.
- it could be really bad for reputation
  - either for customers, or clients who use your service to supply their customers
  - example
    - If AWS S3 goes down, a lot of companies will suffer, including Netflix, and that is not good.


## SLAs - service level agreements

- In order to make online services competitive and meet the market's expectations, online service providers typically offer Service Level Agreements/Assurances.
- These are a set of guaranteed service level metrics
  - example
    - Five 9's uptime
    - latency of request response to a service will be 1 second
    - A service can handle 1000 calls a second
- In many cases failing to meet the SLA will give the customer a right to credits or some other form of compensation for the provider's failure to meet that assurance.
- It is especially important to consider whether availability is in fact a key requirement for a part of a system, and which parts require high availability.

## Design

- When designing a high availability (HA) system, then, you need to reduce or eliminate "single points of failure".
  - A single point of failure is an element in the system that is the sole element that can produce that undesirable loss of availability.
  - You eliminate single points of failure by designing 'redundancy' into the system
    - Redundancy is basically making 1 or more alternatives (i.e. backups) to the element that is critical for high availability.
- Example
  -  if your app needs users to be authenticated to use it, and there is only one authentication service and back end, and that fails, then, because that is the single point of failure, your system is no longer usable.
  - By having two or more services that can handle authentication, you have added redundancy and eliminated (or reduced) single points of failure.
- you need to understand and de-compose your system into all its parts. Map out which ones are likely to cause single points of failure, which ones are not tolerant of such failure, and which parts can tolerate them
  - Because engineering HA requires tradeoffs and some of these tradeoffs may be expensive in terms of time, money and resources.

## Links

- https://en.wikipedia.org/wiki/High_availability
