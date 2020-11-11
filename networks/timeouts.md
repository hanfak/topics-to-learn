# Timeouts

- Socket Timeout
  - The connection timeout is the timeout in making the initial connection; i.e. completing the TCP connection handshake
- Read Timeout
  - the timeout on waiting to read data1. Specifically, if the server fails to send a byte <timeout> seconds after the last byte, a read timeout error will be raised.
- Session Timeout
  - 408 status code

## why have them
