# Transactions

- When systems are implemented in a distributed format, the idea of transactions (ie ACID) becomes hard. Yet some use cases requires a flow that is transactional (ie if one part of the flow fails, then everything is rolled back, there most be some sort of compensation (either db restored to previous state, calls to external services sent to stop it processing or revert the action))
- These are commonly known as SAGA patterns


Common patterns:

- orchestration
- choreography


## Links

- https://youtu.be/C0rGwyJkDTU
