# Non Blocking IO

## What
- form of input/output processing that permits other processing to continue before the transmission has finished.

## Why

- Input and output (I/O) operations on a computer can be extremely slow compared to the processing of data
  - waiting for response to comeback
  - reading or write to a hard disk
- Instead of waiting, we can start this process on another thread, and let the rest of the program continue. When the IO has finished, we can get the result back and apply callback to do something with the result.

## Benefits

- allows for greater utilisation of the CPU, instead of being idle waiting for IO to finish
-  more efficient use of the request threads
- Minimised number of threads required to serve higher number of concurrent requests, reducing the overall context switching overhead.

## Negatives

- Writing non blocking code can take some getting used to
  - Can be hard to read especially when using callbacks
  - Following the logic can be hard
- Your current location in the code may not convey history
  - For debugging, aync io makes it hard to follow
  - In the case of non blocking code, you can be sitting in a given code context in a core dump, left wondering why you are where you are.
  - This makes it harder to come up with appropriate pre conditions and post conditions and makes program correctness harder
- Blocking in the main thread of a program is suicidal
  - You never want the main event loop of your program to block, because if you do, you have essentially starved lots of file descriptors ready for reading or writing for attention.
- Integrating code libraries which are blocking is problematic
- guaranteeing fault tolerance with callbacks (i.e. avoiding the loss of transactions) and dealing with eventual consistency
- Can be redundant if the IO is necessary for everything else to proceed, so added complexity for no need

## Examples

- Netty
- nodejs
- Java NIO
- UI

## Links
- https://blog.codecentric.de/en/2019/04/explain-non-blocking-i-o-like-im-five/
- https://luminousmen.com/post/asynchronous-programming-blocking-and-non-blocking
- https://medium.com/@nayanava.de01/what-the-heck-is-asynchronous-non-blocking-i-o-1161e83235f9
