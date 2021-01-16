# back of envelope

- Aim is to get a rough estimate of users of a system, to decide how to go about designing it

## Terms

- DAU = Daily active users
  - Normally focused on Average
  - Doing activities which are either reads or writes, these are need to be considered separately in design

## Key numbers

| OPERATION  |  NOTE | LATENCY  |  	SCALED LATENCY |
|---|---|---|---|
|L1 cache reference	|Level-1 cache, usually built onto the microprocessor chip itself.|	0.5 ns|	Consider L1 cache reference duration is 1 sec|
|Branch mispredict	|During the execution of a program, CPU predicts the next set of instructions. Branch misprediction is when it makes the wrong prediction. Hence, the previous prediction has to be erased and new one calculated and placed on the execution stack.|	5 ns	|10 s|
|L2 cache reference	|Level-2 cache is memory built on a separate chip.|	7 ns	|14 s|
|Mutex lock/unlock	|Simple synchronization method used to ensure exclusive access to resources shared between many threads.	|25 ns	|50 s|
|Main memory reference|	Time to reference main memory i.e. RAM.|	100 ns|	3m 20s|
Compress 1K bytes with Snappy	|Snappy is a fast data compression and decompression library written in C++ by Google and used in many Google projects like BigTable, MapReduce and other open source projects.	|3,000 ns	|1h 40 m
|Send 1K bytes over 1 Gbps network||10,000 ns	|5h 33m 20s|
|Read 1 MB sequentially from memory	|Read from RAM.	|250,000 ns|5d 18h 53m 20s|
|Round trip within same datacenter|	We can assume that the DNS lookup will be much faster within a data center than it is to go over an external router.|	500,000 ns|	11d 13h 46m 40s|
|Read 1 MB sequentially from SSD disk	|Assumes SSD disk. SSD boasts random data access times of 100000 ns or less.|	100,000 ns|	23d 3h 33m 20s|
|Disk seek|	Disk seek is the method to get to the sector and head in the disk where the required data exists.	|10,000,000 ns	|231d 11h 33m 20s|
|Read 1 MB sequentially from disk	|Assumes regular disk, not SSD. Check the difference in comparison to SSD!|	20,000,000 ns	|~1.2 years|
|Send packet CA->Netherlands->CA	|Round trip for packet data from U.S.A to Europe and back.|	150,000,000 ns	|~9.5 years|

- Picture representation
  - Imagine working on an assignment for college
  - Your brain is the CPU (ie L1 cache) stuff that is in memory, super fast
  - Go to a book on your desk is like RAM
  - Going to a book in a book shelf, is like Disk Memory
  - Going to the library to get a book and making the return trip to your desk at home, is like doing a network call

## Common numbers

- data conversions
  - 1 byte = 8 bit
  - 1024 bytes = 1 Kilobyte
  - 1024 kilobytes = 1 megabyte
  - 1024 megabytes = 1 gigabyte
  - 1024 gigabytes = 1 terabyte
- 1 char = 1 byte
- 1 integer = 4 bytes
  - 32 bit integer
- unix timestamp = 4 bytes
- time
  - 3600 seconds per hour
  - 86,400 seonds per day
  - 2.5 million seconds per month

## Traffic estimate example

- Info to find out
  - avg Number of users using system
  - avg number of actions (read/write) per user
  - Time frame of these
  - avg size of data to read or write
  - The costs of memory/cdn, bandwidth, storage
  - Think about approx avg revenue per user to determine profitablity
- 10 mill DAU for 30 reads = 300 mill read requests
- 10 mill DAU for 1 write = 10 mill write requests
- 300 mill per day = 300 mill/ 86400 = 3472 read req per day
- 10 mill per day = 10 mill/ 86400 = 115 writes req per day
- Memory used
  - 300 mill reads by 500bytes (approx) = 150 Gb total used (size of CDN)
  - For reads, number of data will be less (20% of total) as same data will be read often. This will probably be cached.
    - 150 * 0.2 = 30 Gb to store
  - For data replication, ie data in distributed cache (will affect costs)
    - 30 Gb by 3 replicas = 90Gb
- Bandwidth
  - 300 mill request by 1.5mb size of payload = 450000GB per day
  - Avg data transfer per second is 5.2 gb = 450000Gb/86400
  - Need to cater for variability, as never stable
- Storage
  - Much more will be needed for long term storage ie 10 years, this is average as users leave (data kept x years then deleted)
    - 10 years of data (365 * 10) by 10 mill writes per day at 1.5mb per payload = 55 petrabytes
