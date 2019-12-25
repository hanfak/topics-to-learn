# Distributed File Systems

- A distributed file system is a client/server-based application that allows clients to access and process data stored on the server as if it were on their own computer.
- When a user accesses a file on the server, the server sends the user a copy of the file, which is cached on the user’s computer while the data is being processed and is then returned to the server.
- Ideally, a distributed file system organizes file and directory services of individual servers into a global directory in such a way that remote data access is not location-specific but is identical from any client. All files are accessible to all users of the global file system and organization is hierarchical and directory-based
- Since more than one client may access the same data simultaneously, the server must have a mechanism in place (such as maintaining information about the times of access) to organize updates so that the client always receives the most current version of data and that data conflicts do not arise.
  - Distributed file systems typically use file or database replication (distributing copies of data on multiple servers) to protect against data access failures.
- Examples
  - Sun Microsystems’ Network File System (NFS),
  - Novell NetWare,
  - Microsoft’s Distributed File System,
  - IBM’s DFS
