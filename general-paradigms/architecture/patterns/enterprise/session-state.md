# Session State

- Stateless objects are objects with no properties.
  - Very rare, possible bad design
- stateless server, we are talking about an architecture where the objects do not retain state between requests.
  - Data is not lost between requests
    - store in db
    - but next request does not rely on previous request
    - The server will clear the data for that request and start again
  - the data is somehow temporarily persisted during the business transaction, the process handling the request is terminated and the server resources are freed.
  - A new request can, then, resurrect the temporarily persisted data and continue the business transaction.
- HTTP servers are stateless
- HTTP protocol is stateless
- if we have no state between method calls, it doesn't matter which object services the request
  - Makes it easy to replicate servers
  - stateless servers are very useful on high-traffic Web sites
  - Statelessness allows us to pool our objects so that we need fewer objects to handle more users. The more idle users we have, the more valuable stateless servers are.
- If I only look at books and don't buy anything, my session is stateless, but if I buy, it's stateful.
- Stateful session
  - ie shopping cart, items in cart are preserved between Requests
- Issues with stateful servers
  - Any stateful server object needs to keep all its state while waiting for a user to ponder a Web page.
  - if we do store state we need to always get the same object, so we need to always redirect the request to the object with state
- we can use a stateless server to implement a stateful session
  - Get the best of both worlds

## Session state

- The details of the shopping cart are session state, meaning that the data in the cart is relevant only to that particular session. This state is within a business transaction, which means that it's separated from other sessions and their business transactions.
-  Session state is distinct from what I call record data,
  - record data: which is the long-term persistent data held in the database and visible to all sessions.
  - Session state needs to be committed to become record data
- if  session state is within a business transaction, it has many of the properties that people usually think of with transactions, such as ACID (atomicity, consistency, isolation, and durability).
  - effect on consistency
  - The biggest issue with session state is dealing with isolation. With many fingers in the pot, a number of things can happen while a customer is editing a policy. The most obvious is two people editing the policy at the same time.
- Not all data held by the session counts as session state.
  -  The session may cache some data that doesn't
really need to be stored between requests but is stored to improve performance. Since you can lose the cache without losing correct behavior, this is different from session state, which must be stored between requests for correct behavior.

## Ways to Store Session State
### Client Session state

### Server Session State

### Database Session State
