# Stateless and Stateful

- Is state stored on the backend
- Parts of system can be stateless or stateful
- As a client must I go to specific server to process something
- Style of storing state in an app
  - and relying on the state being there, ow things will break
- Completely stateless systems are rare
  - State is carried with every request
  - ie JWT

## What

- Stateful
  -  Stores state about clients in its memory
  - Depends on the information being there
  - examples
    - caches attached to servers
    - cookies/sessions stored in memory in app
    - load balanced servers, may hit different server which does not know about your session (may have to log in again)
- Stateless
  - Client is responsible to “transfer the state” with every request
  - May store but can safely lose it
    - ie in a database/file
  - still store data somewhere else
  - Can you restart the backend during idle time while the client workflow continues to work?
  - the backend/app can be stateless, but the whole system can be stateful
  - Example
    - instead of storing sessions in app memory, store it in database, thus no matter what instance/replica of the server you go to, it can retrieve the session from the database

## Protocols

- tcp -> stateful
  - maintains the message order etc, if this is lost the connection dies and needs to restart
- udp -> stateless
  - Can come from multiple servers
- DNS (is udp) -> stateless  
- Can build stateless protocol over stateful one
  - http over tcp
    - if tcp connection dies, http will create another one

## Issues
