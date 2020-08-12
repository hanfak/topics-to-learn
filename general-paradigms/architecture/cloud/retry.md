# Retry

- Problem
  - A distributed environment is prone to transient errors due to slow networks, timeouts etc.
  - But these issues typically self-correct and if the action is re-triggered, it’s likely to succeed.
  - In such situations, applications need to handle these transient failures without impacting the end-user experience.
- Solutions
  - Try and try again
    - There are 3 ways to handle transient failures
      - **Stop and Report exception**:
        - If a fault isn’t transient or cannot succeed when repeated, the application could raise an alert and log the exception
      - **Retry immediately**:
        - If a fault is rare, the application could retry the failing request immediately and the request may be successful
      - **Retry with a dela**y:
        - If a fault is caused by connectivity issues or issues that may need a short period, the application could retry the failing request after a reasonable amount of time has passed
    - The time delay and number of retries can be configured to suit the application needs
    - If the request still fails even after the desired retry count, the application could report it as a fault and raise an alert
  - Example
    - It’s your dear friend’s birthday! You want to be the first one to wish them so you call them exactly as the clock strikes 12
    - The phone’s busy… You figure someone beat you to it. You hang up (kind of disappointed)
    - But you also know the phone won’t be busy for too long. So you redial, and this time you get through and wish them.