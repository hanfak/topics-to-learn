# Idempotency

- Where a request is sent which has some side effect, if that request is retried there is a check to see if action (side effect) has already been done and either a message return stating this or same original message is returned
  - retried because of time out from server (microservices, service mesh), or manually resubmitting
- Some times the the actions where only part way done (events) and then failed. When retrying, the action can start from the last successful event and carry on to completion

## How to implement Idempotency
