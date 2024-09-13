# Dead Letter Queue

## What 

- handle message failure
- A queue which other queues (source queues) can target for messages that cannot process (be consumed) successfully.
## Uses

- to set aside and isolate messages that cannot be processed correctly to determine why their
  processes failed
- Instead of trying to process messages that fail until they expire, move them to a dead-letter queue after a  few process attempts.
  - This can reduce load on consumer/queue having to constantly retry the message, save costs if managed service
-  troubleshoot incorrect message transmission operations.

### Examples 

- Configure an alarm for any messages delivered to a dead-letter queue
- Examine logs for exceptions that might have caused messages to be delivered to a
  dead-letter queue.
- Analyze the contents of messages delivered to a dead-letter queue to diagnose software
  or the producer’s or consumer’s hardware issues
- Determine whether you have given your consumer sufficient time to process messages

## Not to use

- to decrease the number of messages and to reduce the possibility that you expose your system to messages that you can receive but cannot process.
- with standard queues when you want to retry the transmission of a message indefinitely
- with a FIFO queue if you do not want to break the exact order of messages or operations