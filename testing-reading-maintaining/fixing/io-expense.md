# How to Deal with I/O Expense

- For a lot of problems, processors are fast compared to the cost of communicating with a hardware device.
  - Hardware is faster compared to communicating over a network
- Other types of IO
  - disk
  - databases
  - file
  - network
  - hardware not close to cpu, ie usb, external drives etc
- There is a lot of gain from improving IO costs

## How

- Caching
  - Caching is avoiding I/O (generally avoiding the reading of some abstract value) by storing a copy of that value locally so no I/O is performed to get the value.
    - Or putting it somewhere with less IO cost then where it was originally retrieved/accessed from
  - The first key to caching is to make it crystal clear which data is the master and which are copies.
    - There is only one master - period.
    - gossip protocol, master/slave protocol
  - Caching brings with it the danger that the copy sometimes can't reflect changes to the master instantaneously
- Representation
  - is the approach of making I/O cheaper by representing data more efficiently.
  - This is often in tension with other demands, like human readability and portability.
  - ie
    - binary representation instead of one that is human readable
    -  transmitting a dictionary of symbols along with the data so that long symbols don't have to be encoded,
    - and, at the extreme, things like Huffman encoding
- pushing the computation closer to the data
  - improve the locality of reference
  - if you are reading some data from a database and computing something simple from it, such as a summation, try to get the database server to do it for you
  - If you are searching or sorting some data, instead of getting it all into memory, ask the database to do it for you and retrieve the results 
