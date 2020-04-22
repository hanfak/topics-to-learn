# Storage

**For software design **

- Storage is about holding information.
- Any app, system, or service that you program will need to
  - store data
  - retrieve data
  - aka 'set, get', 'store, fetch', 'write, read'
- We use a database to achieve this.
  - A database is a software layer that helps us store and retrieve data.
- To interact with storage, you will need to go through some sort of server that acts as an intermediary for you to conduct these fundamental operations.
- Storage can broadly be of two types:
  - "Memory" storage
    - if you leave data in "Memory" then that usually gets wiped away when you shut down or restart, or otherwise lose power.
    - ie RAM
    - On servers, if the data you're keeping track of is only useful during a session of that server, then it makes sense to keep it in Memory
      - ie  a single session may mean when a user is logged in and using your site. After they log out, you may not need to hold on to bits of data that you collected during the session.
    - This is much faster and less expensive than writing things to a persistent database.
  - "Disk" storage.
    - the disk storage tends to be the more robust and "permanent" (not truly permanent, so we often use the word "persistent" storage instead)
    - Disk storage is persistent storage.
    - when you save something to Disk, and turn the power off, or restart your server, that data will "persist". It won't be lost.
    - ie hard disk, usb pens
    - whatever you do want to hold on to (like shopping cart history) you will put in persistent Disk storage. That way you can access that data the next time the user logs in, and they will have a seamless experience.
    - Or to be used elsewhere at another time
- Factors to consider for storage
  - the shape (structure) of your data
  - what sort of availability it needs (what level of downtime is OK for your storage)
  - scalability (how fast do you need to read and write data, and will these reads and writes happen concurrently (simultaneously) or sequentially) etc, C
  - Consistency - if you protect against downtime using distributed storage, then how consistent is the data across your stores?
- 
