# Circuit Breaker

- Problem
  - There are situations where failures can be caused by unexpected situations and take relatively longer to fix. Retry or waiting for the request to timeout may not be the best option as it may cause further cascading issues such as resource contention and/or blocked threads.
- Solution
  - Fail fast
    - How it works
      - Prevent the application from retrying an operation likely to fail
        - A circuit breaker acts as a proxy that monitors recent failures of an operation
        - The proxy maintains a count of failures and if it crosses the set threshold, it’s placed in an Open state
        - In the Open state, the request fails immediately and is handled appropriately by the application
        - However, limited requests are still allowed to pass through to check if the operation is still failing or has been successful (fixed)
        - If the operation continues to return failures, the Open state continues
        - If the operation was successful, it is assumed the issue has been fixed and the circuit breaker switches to Closed state
        - Error and failure handling in this pattern requires careful consideration to create an acceptable end-user experience
    - Example
      - This pattern is inspired by the actual circuit breaker present in the electrical lines at home or office
      - Electrical Circuit breakers are a protective measure against damage to a circuit in the event of an electrical current overload
      - It connects to your circuit board and interrupts the flow of electrical current if it detects a fault in the flow
      - In the event of a fault, the breaker switch automatically goes off and stops the electricity from flowing through the circuit (Open)
      - Without circuit breakers, in the event of a power surge, you’d be left with blown fuses
      - With a circuit breaker, all you do is unplug some of the appliances that caused the power surge, and flip the circuit breaker switch back to the “on” position (Closed)
      - 