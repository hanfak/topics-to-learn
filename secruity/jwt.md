# JWT

- JSON Web Token (JWT) is an open standard (RFC 7519) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object
- can be verified and trusted because it is digitally signed
- can be signed using a secret (with the HMAC algorithm) or a public/private key pair using RSA or ECDSA.
-  can be encrypted to also provide secrecy between parties, not necessry
  - prevents others seeing the contents
- When tokens are signed using public/private key pairs, the signature also certifies that only the party holding the private key is the one that signed it.

##  Uses

- Authorization
  -  Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token.
  - allowing the user's identity to be established and maintained across multiple requests.
  -  allowing the identity of the user or client to be passed between systems without the need for additional database lookups.
- Single Sign-On (SSO)
  -  allowing a user to log in once and obtain a token that can be used to authenticate them across multiple systems
- API Security
  -  secure RESTful APIs by transmitting information about the user and their authorization level to protected endpoints.
- Microservices Communication
  - used to securely transmit information between microservices in a microservices architecture.
- Information Exchange
  -  way of securely transmitting information between parties, asymmetric encryption
  - verify that the content hasn't been tampered with.

## Structure

- consist of three parts separated by dots (.)
```
xxxxx.yyyyy.zzzzz
```
- Header
  - typically consists of two parts:
    - the type of the token, which is JWT
    - the signing algorithm being used, such as HMAC SHA256 or RSA.
  - base64 encoded
  ```json
  {
    "alg": "HS256",
    "typ": "JWT"
  }
  ```
- Payload
  - contains the claims
  - Claims are statements about an entity (typically, the user) and additional data.
    - Three types
      - Registered claims:
        - are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims.
        - Some of them are: iss (issuer), exp (expiration time), sub (subject), aud (audience), and others.
      - Public claims:
        - can be defined at will by those using JWTs. But to avoid collisions they should be defined in the IANA JSON Web Token Registry or be defined as a URI that contains a collision resistant namespace.
      - Private claims:
        - are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.
    - is readable
      -  Do not put secret information in the payload or header elements of a JWT unless it is encrypted.
    ```json
    {
      "sub": "1234567890",
      "name": "John Doe",
      "admin": true
    }
    ```
- Signature
  - To create the signature part you have to take the encoded header, the encoded payload, a secret, the algorithm specified in the header, and sign that.
  - ie
  ```
  HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  secret)
  ```
  - used to verify the message wasn't changed along the way, and, in the case of tokens signed with a private key, it can also verify that the sender of the JWT is who it says it is.

## How to use

- Issuance
  - The server generates a JWT and sends it to the client, typically after the client has provided valid authentication credentials.
  - This can be given via a separate AuthO server (using openid)
- Transmission
  - The client sends the JWT in subsequent requests to the server, usually by including it in the Authorization header.
  - `Authorization: Bearer <token>`
- Validation
  - The server receives the JWT and verifies its signature, ensuring that the token was issued by a trusted source and that the contents have not been tampered with.
- Decoding
  - The server decodes the JWT and extracts the payload, which contains the information about the user or client, such as their identity and authorization level.
- Processing
  - The server processes the request based on the information contained in the JWT, such as granting or denying access to a particular resource.
- Renewal
  - If the JWT has a short expiration time, the client may need to request a new JWT after a certain amount of time has passed.

### Best practice

-  using secure algorithms and keys
- Validate the Token
  - Validate the contents of the JWT to ensure that the token was issued by a trusted source and that the contents have not been tampered with.
- using a secure method of transmitting JWTs (such as HTTPS).
- Short Expiration Time
  - Set a short expiration time for JWTs to minimize the risk of a compromised token being used for an extended period.
- Stateless
  - Design your implementation to be stateless to reduce the risk of sensitive information being stored on the server.
- Limit Data
  - Store only the minimum amount of data necessary in the JWT, and avoid sensitive information such as passwords.
- Logging and Monitoring:
  - Log and monitor JWT-related activities, such as token issuance and validation, to detect and respond to potential security incidents.
- Regular Key Rotation
  - Regularly rotate the keys used to sign JWTs to minimize the risk of a compromised key being used for an extended period.
- Access control
  - Implement proper access control mechanisms to ensure that JWTs are used appropriately and that users are not granted excessive permissions.

## Downsides

- Size can grow to be big
  - if there is a lot of information encoded within them, which can have an impact on network performance.
- Security:
  - If a JWT is not properly secured, it can be intercepted and used by an attacker.
  - In addition, if the secret used to sign the JWT is compromised, the attacker can generate their own JWTs. ie private key is exposed
- Statelessness:
  - JWTs are stateless, there is no way to invalidate a token once it has been issued.
  - make it difficult to manage situations where a user's permissions change, or when a user needs to log out.
- Scalability:
  - can put a burden on the authentication and authorization process if the number of requests is very high, as each request requires the JWT to be processed and verified.
- Flexibility:
  - JWT is designed to be compact and self-contained, which can limit its ability to transmit complex information structures or data relationships.

### Security exploits

- Secret Management:
  - The security of a JWT depends on the secrecy of the secret used to sign it. If the secret is compromised, an attacker can generate their own JWTs and impersonate the user.
- Tampering:
  - JWTs are signed but not encrypted, which means that the contents of the token can be easily read by anyone who has access to it.
  - If a JWT is tampered with, the signature will no longer match, which can alert the recipient to the tampering.
- Token Replay:
  - JWTs are stateless, there is no way to invalidate a token once it has been issued.
  - This makes it possible for an attacker to replay a token and gain unauthorized access.
- Brute Force Attacks:
  - If the secret used to sign JWTs is weak, it can be vulnerable to brute force attacks, where an attacker repeatedly tries different secret values until they find the correct one.
- Insufficient validation:
  - If the recipient of a JWT does not properly validate the contents of the token, it can result in security vulnerabilities, such as authorization bypass or data tampering.

## Benefits

- Stateless
  - JWTs are stateless, meaning that the server does not need to store any information about the user or client, reducing the server's load and improving scalability.
- Standardized
  - JWT is a standardized format, which makes it easy to integrate with a variety of technologies and platforms.
- Easy to Use
  - JWT is simple to use and can be transmitted over the standard HTTP header, making it easy to implement and integrate into existing systems
- Speed
  - JWT enables fast and secure authentication and authorization, as the server only needs to verify the signature of the token, rather than perform a database lookup.
- Portability
  - JWT can be used across multiple domains and platforms, allowing for a seamless user experience and improved interoperability.
- Compact
  - JWT is a compact format, which makes it efficient for transmitting information over the network.
  - use of json
- Flexibility
  - JWT can carry a variety of information in its payload, allowing for a flexible and customizable authentication and authorization experience.

## Alternatives

- OAuth 2.0
  - A widely used standard for authorization that enables users to grant access to their data without sharing their passwords.
- SAML (Security Assertion Markup Language)
  - An XML-based standard for exchanging authentication and authorization data between parties.
- Cookies and Sessions
  - A traditional approach to authentication that uses a server-side session to store user data and a client-side cookie to track the session.
- API Key
  - A simple authentication method that uses a unique key to identify the client and grant access to an API.
- OpenID Connect
  - A simple identity layer built on top of OAuth 2.0, which enables users to authenticate with a single identity provider and access multiple applications.

## Links

- - https://jwt.io/introduction
