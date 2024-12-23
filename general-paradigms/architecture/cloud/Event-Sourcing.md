# Event Sourcing & CQRS

- Problem
  - When interacting with data, most applications store the current state of the data.
  - Updates to the data elements are typically overwritten by the latest.
  - If one wanted a history of all the updates, the application would need to be built to maintain history tables.
  - Every time an update request is made, the current data would be moved to the history table before being overwritten.
  - This adds to the overhead of having a robust historical backup and ensuring the application scale plan includes scaling the historical stores as well.
- Solution
  - Event Store
    - How it works
      - Define application change as a sequence of events and record them in an event store in the sequence they were applied (an audit trail)
      - The events are immutable and stored as append-only but can be published to consumers who may process them as required
      - This model not only stores the history of the state of the application but also allows a replay of those events to obtain the current state of the application — one of the following
        - A complete rebuild
        - A point in time rebuild
        - Reverse events
      - The trick here is dealing with external systems in a manner where they do not know the difference between real transactions and replays
  - example
    - Event sourcing works a lot like Book Keeping: A bookkeeper will log the day’s financial transactions such as payments, receipts, purchases etc made by an organization and document it within either a supplier or general ledger
    - All the financial events, money-in and money-out are now available in these ledgers (..the audit trail)
    - An accountant can use this information to create reports for any custom time-period
    - Going through the transactions (replay), the accountant could potentially recreate the same report multiple times and still get the same result for that specified period

## Links

- https://youtu.be/i2eVTk2Fb40
- https://codurance.com/2015/07/18/cqrs-and-event-sourcing-for-dummies/
- https://martinfowler.com/eaaDev/EventSourcing.html
- https://axoniq.io/resources/concepts
- https://completedeveloperpodcast.com/episode-134/
- Event Sourcing - You are doing it wrong – David Schmitz https://www.youtube.com/watch?v=UevquaeEJ8c
