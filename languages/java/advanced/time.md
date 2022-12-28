# Time in Java
- https://stackoverflow.com/questions/32437550/whats-the-difference-between-instant-and-localdatetime
Time is awkward in code. In reality you cannot fix the actual time, it just keeps on going.

There are different ways of representing time in java, some are best practice, some are legacy, some have issues:
- instant
- LocalDate
- LocalDateTime
- LocalTime
- ZoneDateTime
- Date

- The problem with time, comes with internationalisation, workign with time in different timezones, and especially when doing things between to things in different timezones.
- we have another issue of daylight savings
- Due to this complexity and current time is never fixed, the chances of creating bugs are high. Thus we need ways of being able to test code that deal with time
- To handle legacy
  - either convert or do a full migration to Time package
  - Might be using JodaTime, which is not actively worked on, so best to migrate to Time package

## Testing time

- In general, we can use the same ideas of DI and mocking to control time
  - We consider the act of getting the current time (ie Instant.now()) as a service behind an interface
### Links
- amigos code
  - https://www.youtube.com/watch?v=PrPQ5xHYa0s

## Issues
- SimpleDateFormat is not thread safe when sharing this object between threads
  - Need to instantiate a new object for each thread
  - Use FastDateFormat from apache commons, which is threadsafe
  - https://www.youtube.com/watch?v=JdNQoTJmzis Java's SimpleDateFormat is a Disaster Waiting to Happen

## Links

- https://www.youtube.com/watch?v=0XgdX5hDL4U Java basics of the LocalDate, LocalTime, LocalDateTime, ZonedDateTime and the DateTimeFormatter
