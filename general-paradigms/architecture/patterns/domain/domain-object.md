# Domain Object

- domain object as an object with an identity that is loaded from the database, manipulated for a certain use case, and then stored back into the database, usually within a database transaction.
- One domain object can just be used only for use cases and separate domain object is used for persistence
  - As database may need different fields compared to the usecase
- Can have behaviour based on the state of the object
- Can have validation on the construction of the object
