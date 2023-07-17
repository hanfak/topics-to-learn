# Event Driven Architecture

- https://youtu.be/DQ5Cbt8DQbM
- https://martinfowler.com/articles/201701-event-driven.html
- https://www.youtube.com/watch?v=STKCRSUsyP0
- https://moneystock.net/wp_e/2021/05/28/4-types-of-event-driven-architecture-by-martin-fowler/
- https://youtu.be/DQ5Cbt8DQbM
- https://www.datamachines.io/blog/asynchronous-thinking-for-microservice-system-design
- https://www.alexdebrie.com/posts/event-driven-vs-event-based/
- 
## Consistency 

- When publishing events to a queue, we normally store that event in a db (to have replayability)
  - Unfortunately, if the event is sent off to the queue before being persisted, 
    - then the message could be sent off but the db might fail -> so if there is a failure that needs to be replayed, it cannot
    - or the event is sent and processed by another consumer, but needs the data from the db (which might not have been persisted before the next consumer needs it)
  - To solve -> store the event (or details) in the db before publishing
- But this solution (save before publish) can have issues too 
  - as the message broker could be down, and thus the event is never sent 
  - solution -> fallback 
    - if the message does not reach the broker add it to a another table in db and have another service (with cron job) to read from and publish it to the broker 
      - this can involve retry mechanisms 
    - could also put it on a retry queue, where the broker handles the schedule
    - issues 
      - message can be out of order
  - solution -> outbox
    - when sending the event, just store in the database
    - Then another service on cron job, will grab the event (or details to make an event) from the db, and publish it
    - can invovle retries and fallback
    - once succesfully published, can update record or delete from db, so not republished
    - Issues 
      - can put extra load on db