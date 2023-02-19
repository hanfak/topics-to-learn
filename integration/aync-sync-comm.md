# asynchronous and synchronous communications

- Can I do work while waiting?
  - yes -> asynchronous
- History
  - everythign was synchronous

## synchronous IO

- the caller waits for a response from receiver
  - E.g. Asking someone a question in a meeting
- Caller sends a request and blocks Caller
  - must wait for request to finish processing until it continues
  - Caller cannot execute any code while waiting
  - caller/client and receiver/server are in sync
- When the request is made to fetch the data, the cpu is waiting for the hardware/network to do it's thing and return with the data.
- ie IO - files, http requests
- Example
  - Program asks OS to read from disk
  - Program main thread is taken off of the CPU
     - As the cpu is waiting for the file to be read from the hard drive, it can context switch and do something else, but the program is still waiting for the cpu to finish processing
  - Read completes, program can resume execution

## Asynchronous IO
-  the response can come whenever. Caller and receiver can do anything meanwhile
- flow
  - Caller sends a request
  - Caller can work until it gets a response (cpu context switches)
  - Caller either:
    - Checks if the response is ready (epoll)
    - Receiver calls back when it's done (io_uring)
    - Spins up a new thread that blocks, while the main thread carries on processing
      - Thread finish reading and calls back main thread
  - Caller and receiver are not necessary in sync

### Examples

- Asynchronous Programming (promises/futures)
- Asynchronous backend processing
  - flush to queue with job id, and some call (poll, push) checks the job id to see if complete
  - client sends work for backend to do, the client can still carry on processing, but it is still waiting for the backend to comeback with the completed work
    - from client perspective it is aysnc, but the backend is sync
- Asynchronous commits in postgres
  - To do with transactions (executing multiple actions) and the commit confirms all of them if they were all validated and no failures
- Asynchronous IO in Linux (epoll, io_uring)
- Asynchronous replication
- Asynchronous OS fsync (fs cache)

## Clients

- in past, they were synchronous/blocking
- Now most of them are aysnchronous

## Links

- https://www.fridayfeedback.com/p/asynchronous-communication/
- https://dzone.com/articles/microservices-why-asynchronous-communications
- https://dzone.com/articles/communicating-between-microservices
- https://danieltammadge.com/2021/01/event-driven-vs-request-driven-architecture-user-registration/
