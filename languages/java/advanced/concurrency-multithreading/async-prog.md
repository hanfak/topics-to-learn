# Asynchronous Programming

- why is asynchronous programming needed at all? Only to prevent the blocking of threads, because threads are expensive.
- project Loom Java designers are working on virtual threads (aka fibers/lightweight threads) which will aim to significantly reduce the cost of threads and thus eliminate the need of asynchronous programming.

## Synchronous Vs Aysnc

- https://stackify.com/asynchronous-programming-easier-think/

## Using completeable futures

- http://www.deadcoderising.com/java8-writing-asynchronous-code-with-completablefuture/
- https://mjg123.github.io/2017/10/23/Java-Futures-Promises.html
- http://www.deadcoderising.com/java8-writing-asynchronous-code-with-completablefuture/
- http://www.deadcoderising.com/java8-writing-asynchronous-code-with-completablefuture/
- https://youtu.be/ImtZgX1nmr8
-
### Timeout java 8

- http://iteratrlearning.com/java9/2016/09/13/java9-timeouts-completablefutures.html
- http://www.deadcoderising.com/timeout-support-using-executorservice-and-futures/
- http://vaughndickson.com/2016/07/05/how-to-timeout-a-thread-in-java-limiting-a-threads-execution-time/

## Why no async/await

- Java try to eliminate the need for asynchronous methods instead of facilitating their use.
- asynchronous programming using CompletableFuture causes three main problems.
  - branching or looping over the results of asynchronous method calls is not possible
  - stacktraces cannot be used to identify the source of errors, profiling becomes impossible
  - it is viral: all methods that do asynchronous calls have to be asynchronous as well, i.e. synchronous and asynchronous worlds don’t mix
- async/await solves the first problem it can only partially solve the second problem and does not solve the third problem at all (e.g. all methods in C# doing an await have to be marked as async).


## Within the app

## outside the app

- A User access the app, and the response/output is returned straight away without any processing being waited for.

### Why

- Processing might take longer than expected, and timeouts and wait time to long. So send an automatic reply.
  - If something goes wrong, then we inform the user some other way
## links

-  http://www.gq-magazine.co.uk/article/margate-city-guide-travel-tips
