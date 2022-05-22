# Event loop

- What the heck is the event loop anyway? | Philip Roberts | JSConf EU https://youtu.be/8aGhZQkoFbQ
- Node.JS contains a "dispatcher." It accepts web requests and hands them off for asynchronous processing. That dispatcher is single threaded. But the dispatcher spins up a new thread for each task, and quickly hands off the task to the new thread, freeing the dispatcher's thread for servicing a new request.

To the extent that those task threads are kept separate (i.e. they don't modify each other's state), yes, they are threadsafe.
