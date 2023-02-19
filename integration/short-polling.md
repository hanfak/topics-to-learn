# Short Polling

- Request is taking a while, I’ll check with you later
- checking if this thing is done
- Letting the backend handle it (aysnc), and it receives a response with some id, which it can use to send more requests to check if the job has been completed (and/or get some data)

## Uses

- A request takes a long time
  - uploading a large file
- Backend wants to send a notificaiton

## How

-  Client sends a request
-  Server responds immediately with a handle( id/callback)
  - but server can process it whenever
- Server continues to process the request
- Client uses that handle to check for status
- Multiple “short” request response as polls

## PRos

- simple
- Good for long runnign requests
- client disconnects
  - can save request id from long running request, and can start up again (on app start up, or cron job)

## Cons

- Too chatty -> Increased network bandwidth
  - Especially with scaling, with one client is fine, but as the number of clients increase can overwhelm the server and bandwidth
- Wasted backend resources
  - Instead of checking, it could have done other things 
