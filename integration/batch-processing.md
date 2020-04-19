# Batch Processing

- We normally prefer our applications that respond to user input directly
  - but there are usually at least a few processes that happen out of band (aysnchonously) or even overnight

## Why

- sending emails in bulk, importing large amounts of data from external systems (or pushing data to external systems), or for managing outages and latency in external services.
- Handling interactions with unstable, slow, or limited third-party systems is often best handled with a batch process
- many industries have a tendency to prefer batch processing to processing-as-needed.
  - Banks and regulated industries
- used to shift system workloads into time periods where utilization is lower.

## Startup

- How often and where does this thing run?
  - Should not run on local machine, or machine with low or out of date spec
    - This leads degenerating processes and failures
    - Can be accidentally unplugged or power surge
  - Questions to ask
    - Are all your servers available at the time of execution?
    - Are they running intense batch processes themselves?
    - What about the databases you are using?
    - Is maintenance being performed on them during this time window?
    - What about time zone issues?
    - Could your application’s scheduled run time be missed during a shift to day light savings time?
    - Could a forced system update occur during your startup window?

- What resources are available during the run?
  - How much memory, disk, and network I/O are available?
    - doesn’t mean that they will be available when it starts up.
    - This could impact how long your process takes to start up or whether it can even start at all.
  - Sometimes systems are turned off or otherwise unavailable after hours.
    - work systems will be turned off entirely after hours, especially if you are using a cloud environment. Third party systems may be under similar constraints

- How do we handle failure to start up?
  - Sometimes the task scheduler chokes and crashes. Permissions can also change, which could stop your program from running. Your application might start loading and then fail before actually starting processing
  - This could result from anything to not having all of its dependencies available, to simply not being able to contact the system that it uses to determine what work needs to be done.
  - If your app fails to start, you cannot rely on your app to tell you that it didn’t start.
    - This means that you have to have some kind of monitoring process in place to let an admin know if the process fails to run.
    - It also means that system is a potential point of failure, especially if your code crashes due to it being down. You don’t want to write your own tools for this.

## Loading

- How do we retrieve the list of work items?
  - One of the first steps you batch processor will perform is the retrieval of a list of items to process
    - This tends to mean accessing a database, the file system, a durable message queue, or making a network call to some other service
    - This is an additional point of failure,
    - you may want to have retry logic here so that a small transient fault doesn’t stop the whole thing from running.
      - If you implement retry logic, you need to wait some time and try again. You should not try again immediately, as this is likely to fail and can transform transient issues into much more serious problems.
      - You also probably shouldn’t just retry forever. Sometimes systems are just down and there is nothing you can do.
  - You might simply have no records to process. If your application treats this as a failure or tries to read some value it needs from the first record in the set, this is a problem.
  - our application might also receive malformed data in the dataset that it gets back.
    - This might be changed by someone else
  - Be especially careful about SELECT *, or about referencing columns by position in a result set.

- How do we make sure that we don’t retrieve too many work items to process?
  - Can happen either as the
    - result of an attack,
    - a mistake by a developer, or
    - because the application you are supporting has grown,
  - you need to make sure that you limit how many records you load into memory at a time.
    - Besides making startup slow, you can very easily run out of memory by attempting to load too many records.
    - You may also put excessive pressure on the database server or network during this step.
    - The best way to do this is to track which records your process has grabbed and which ones have completed processing, along with a processor identifier and a timestamp for when you started (so that you can easily track failures)
    - make your processing logic idempotent, so that nothing bad happens if a record is run twice.
  - breaking up the workload into chunks makes some other things easier
    - you may need to eventually have multiple instances of the batch process running. It’s easier to do that if the first version is built in such a way that it doesn’t grab everything.
    - makes restarting the process a bit easier, as you can just grab the records that haven’t completed processing.
    - makes it easier to see if a particular processor has an issue, or if a transient issue appears frequently at a certain time, or after a certain number of records has been processed.

- How do we make sure that items that can’t be processed are marked?
  - You need to keep track of items that failed to process more than a couple of times
    - This will keep you from having to store that state in memory, which means that you can scale up to multiple instances easier.
    - makes manual interventions easier later on, since you can easily query for the items that fail
    -  to record each failed attempt in a queryable manner for easier troubleshooting during business hours.
  - consider an archival process as well.
    - Over time, failed work items will pile up in the system (think failed bank transactions), making the system slower over time.
    - You should probably have a way to move failed work items off to some other storage after a time limitation has been met so that they don’t pile up and slow down ongoing work.

## Running

- How (and to whom, and by what mechanism) do we deal with critical errors?
  - a system is built to run unattended does not mean that failures can be unattended
  - If the process is crucial enough to business continuity, then somebody has to find out about errors that occur during processing.
  - alerting
    - should be configurable without redeployment, and
    - also needs to be resilient to transient errors of its own.
    - If your app has built in retry logic for transient failures, you probably don’t want to send alerts about a failure until a failure limit has been hit (due to the numbing effect of false positives).
  - If the security environment has changed and caused a failure, it may also stop you from reporting that failure.
  - If a bug in an updated version of the app causes a hard failure, it’s entirely possible that this failure will prevent the reporting of errors as well
  - Error reporting and diagnostics of a failure might also fail themselves, so you need to make sure these failures don’t take down the app if it can otherwise continue processing.

- How do we deal with transient errors during processing?
  - Sometimes you’ll get a “blip” while processing and a retry will fix it.
    - Transient network, database, and file system errors can often be recovered from by retrying in a few minutes.
  - Since this processing is unattended, you probably should implement retry logic in your application
  - Don’t retry immediately though – use a incremental backoff system so that if transient errors occur, you aren’t putting undue strain on other parts of the system.
  - There will be certain points in the lifecycle of your offline processing app where most of the transient faults you encounter are due to load in one way or another
  - Things like the circuit breaker pattern are helpful for this. When calling services external to your batch process, make sure that you take instrumentation around how long calls are taking.
  - This makes it easier to rule out problems with external systems when your system’s performance is suffering.

- How do we intend to scale our workload if necessary? Will we support multiple instances?
  - running a job out of band, you probably should be considering scale from the outset
  - out of band processing is done because it makes it easier to smooth out problems with load.
  - If it takes more resources to run a batch process than it does to take whatever action triggers that process, it’s a likely point of failure in your architecture under load, so you need to think about this in advance
  - Also watch for dependencies.
    - Some of them will have hard limits on the load you can put on them without an additional fee, or may even start rejecting requests.
  - Cost of failure. How much latency is acceptable? Cost per item processed (look at the average, and the range encompassing three standard deviations if these vary).
  - How soon does your organization obtain value from processing, versus how long it takes to get charged for the processing
    - if you pay your server bills monthly, but it takes six months for your clients to pay you, the pain is there a long time before the medicine is

## Stopping

- What triggers job termination and how do we handle it gracefully?
  - From the outset, you should figure out how long is an acceptable run of a batch process.
    - Sometimes long-running processes will hang or will develop extreme latency as a result of situations beyond your control.
    - If they aren’t supposed to still be running during business hours, you need to figure out what to do
    - Your task scheduling system may be able to automatically terminate long-running jobs, but these are often not particularly clean in the way they kill the job.
    - You may instead opt for a configurable time limit for the batch process, and terminate at a logical point in the code where you are unlikely to produce errors.
    - Hard-killing a running process is generally a bad idea, as you could easily leave your system in an inconsistent state if not careful.
  - At shutdown
    - You may need to simply roll back a database transaction or two if you are lucky and everything is on-premise and in a single database
    - If you are using multiple databases that you own and processing is across databases, it’s entirely possible to end up in a state where data has been committed to one database, but has to be rolled back in the other. You may have to write your process in such a way that you can detect and correct this.
    - If your system makes calls to external services and stops halfway through, you’re going to need to find some way of recovering from a partial completion, especially if the external service costs you or your clients money
    - Try to keep anything you are doing idempotent, if possible, or at least do so for as much of the work as you can.
- What happens if the job runs longer than expected?
  - need to consider what the consequences of a long job run are.
  - if you are batch processing financial transactions, will a slow job processor mean that the transactions take place in a different day?
  - You might also consider downstream problems. What happens if the payment is due today, but the processor ran too long and the transaction actually processed with tomorrow’s date on it? Could this trigger a late fee? If the process runs too long, will it (or should it) start picking up work that was queued up during the current run?
  - consider load issues.
    - If the process is intensive in terms of system resources (like video processing), what happens if the run extends into normal business hours when the people in suits want the system to be snappy?
    - What about any artifacts produced by the process (such as reports)? If they aren’t ready on time, how do humans that need that data proceed?
    - Will external services start acting differently if processing runs over on your end?
    - Could you hit rate limits for external services if both the batch process and your normal business processes are running concurrently? What’s the cost?
- How should the process report its results?
  - When a process completes, is there anything produced that human beings need to deal with?
    - Typically at the very least, there will be some data that will need to be updated to indicate a successful run and what resulted from it
    - You may also need to report failed work items, and even performance issues encountered along the way.
    - Admins will also generally need to know if there were failed work items, and for whom, so that they can deal with the results.
  - how the data that your end users need will be retrieved.
    - build out reporting tables and aggregate the required data beforehand, rather than putting load on servers during normal operating hours.
      - especially true if the data is scattered across numerous places, or is difficult to aggregate in some way.
    - If you send data to human beings and your process is delayed, you might also want to send some kind of notification that the reporting will be delayed if it is.
