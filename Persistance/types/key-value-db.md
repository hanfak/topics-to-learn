# Key value database/store

## What?

- is a data storage paradigm designed for storing, retrieving, and managing associative arrays, and a data structure more commonly known today as a dictionary or hash table
  - where each key is associated with one and only one value in a collection.
  - The value can be any kind of data like an image, user preference file or document. The value is stored as a blob requiring no upfront data modeling or schema definition.
  - The storage of the value as a blob removes the need to index the data to improve performance. However, you cannot filter or control what’s returned from a request based on the value because the value is opaque.
- key-value stores have no query language
- hey provide a way to store, retrieve and update data using simple get, put and delete commands; the path to retrieve data is a direct request to the object in memory or on disk.
  - The simplicity of this model makes a key-value store fast, easy to use, scalable, portable and flexible.


- https://www.aerospike.com/what-is-a-key-value-store/
