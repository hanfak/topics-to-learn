# Communication Between Two Applications via TLS

- Communications via https (tls/ssl protocol)

Some defintions
  - Client(C) is the application that sends a https request to Server(S)
  - Server has an open port that accepts https request from a Client

- Issues
  - Two applications (C and S) can communciate over HTTP (via tcp/ip) over a network, but the data can be seen at stage through the network transfer (ie at routers, man in the middle spying etc).
  - Even secure networks (internal only) may not be secrue, we may not want certain internal people/apps to view the transfer of data

- Implementation of HTTPS
  - A Server, must have Public Key certificate (which is signed by trusted CA- normally an intermediary) and a Private key (which is never shared)
  - during SSL handshake, the server sends the public certificate to the Client
  - The Client has Certificate of the Root/Intermediary which it uses to know it can trust any response from a server.
  - The Client receives the public cert from the Server, it checks the chain of the site specific cert, which sends it to another cert (the intermediay on the same public cert), then on to another cert which should be the certifcate on the Client side.
  - If all certs match up, it allows the transfer of a private key, so both Client and Server and can use to encrypt and decrypt communciations, and then http can be begin


- Implementation of HTTPS via nginix
  - server accepts http requests, but nginx accepts https and translates to http and routes it on to the application Server
  - The client sends the http request, nginx transforms it to https and sends it across the network
  - Use of nginix depth setting, allows the nginx to look at the cert chain to check the server has provided the cert and it follows the chain to the intermediate (which is attached to the provided cert) and the next chain (which is on the client). If it can do that in the number of depth, it will confirm identity of server and allow communication

- Implementaiton of HTTPS via JKS
  - Server side
    - Once a public certificate (digitally signed) and private key is created
    - We can use the keytool command to create a keystore
    - This Keystore which ships with the application as a resource is used by the Server (embedded or external) to handle HTTPs communication
  - Client side
    - The client needs to have a public(is root cert public???) certificate of a cert in the chain which the server will present it with.
      - generally the intermediate or root
    - This is created by the keytool to create a truststore jks file
  - Putting the chain on the certificate ?????
