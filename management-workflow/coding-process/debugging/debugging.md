# Debugging
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 updateOnSave:1 orderedList:0 -->

- [Debugging](#debugging)
	- [From bug in a running application in production](#from-bug-in-a-running-application-in-production)
	- [From a failing build](#from-a-failing-build)
	- [From test not passing correctly](#from-test-not-passing-correctly)
	- [Within container or application is running](#within-container-or-application-is-running)
	- [Debugging Issues With memory or high requests](#debugging-issues-with-memory-or-high-requests)

<!-- /TOC -->
## From bug in a running application in production

## From a failing build

## From test not passing correctly

## Within container or application is running

## Debugging Issues With memory or high requests

- Need metrics to cover a long period
- Need to see metrics from the jvm
  - Threads in use
    - This should not be increasing continuously, but go and down to show that the threads are being closed
  - Heap memory
    - Should show the memory being garbaged collected
- Need time taken to return a response
  - Is it just one endpoint, or all end points?
  - Is it one instance of the app or several or all?
  - Does it increase in latency? then drops?  Then increase again
- If cannot get metric needed, maybe way of getting metrics is down,  need to check the metrics trend before it stopped producing metrics
- Get the heap dump
  - `jps` - to get the PID
  - `jstack <pid>` - to get the trace
  - Need to get the full trace, in a file
  - Go to intellij, and copy the file contents into the `analyze` -> `analyze stack trace` and look at the info.
    - Look for any info that might appear in your app ie thread names that are used in your app or classes in your app
- Get the problem on your local box. Run the app, get trace, compare to the trace from the environment that had the problem.
  - use an end to end test and debug
- Maybe the problem is a one off, and looking at the trend, wiil show this
