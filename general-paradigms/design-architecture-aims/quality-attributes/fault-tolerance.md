# Fault Tolerance

- An airplane has 4 engines, if one fails, can still use the other 3.
- A fault tolerant system
  - need to anticipate the faults
  - manage the failures
  - prevent the failures
  - monitor the system for the faults and failures, for warning signs and when they occur
  - How to fix it
  - How to fail gracefully
- https://www.future-processing.pl/blog/how-to-build-a-fault-tolerant-system/
- https://dzone.com/articles/fault-tolerance-is-not-high-availability
- https://dzone.com/articles/make-services-fault-tolerant

## Fault vs failure

- Fault is a cause of failure
- Failure is the effect
- https://youtu.be/7vIzGmxdUvI

## Fault prevention

- Preventing faults from occuring
- Need some form of monitoring of what could go wrong
  - Alerting when when going into danger zone, and in danger zone
  - Thus can be fixed (manual or automated)
- Backups, to replace problem issue
  - removal and replacement of problem issue

## Fault handling

- Includes fault tolerance
- How to handle the failure, in a better way then exiting or breaking down
- Maybe give some between result, but not the expected result
  - Out of date, default
  - time it takes to produce result is longer (use of queue)
  - replicas to share load

## Fault fixing

- Use of metrics, logs
- Find issues
- Short term fix, manual intervention - data fix or hit an endpoint
- Long term fix  
  - Code fix
- Triage and investigation, so this can be prevented, fix can be automated (or done faster when spotted), fixed permemently

## Types of faults

-Categories
  - Transient
    - occurs for a very small duration
    - hard to locate
  - permanent
    - continues until fixed
    - easier to identify

- Human/code fault
  - Fix:
    - before release - testing, requirments met, requirements are correct from business
      - Not all faults can be caught
    - AFter release - nice failure message to user, no crashing, good logs with more details about that failure for techops or devs to help resolve issue, if known issue can deal with appropriate response, if unknonw need to deal with through investigation and quick fix but need to triage to decide on automated or manual process for this issue
- Hardware fault
  - Fix: Replication or backups
- Network fault

## Types of failures

Effects could be

- requests are return 500 responses
- System acts in erratic state
- Server shuts down
- Processing of request is slow, even stops, as throughput increases
- Wrong response
- Use of wrong data
- One component stops working, cascading to whole system failure
