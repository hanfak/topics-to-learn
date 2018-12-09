# Secruity

## Certificates

- client cert
  - https://www.websecurity.symantec.com/security-topics/client-certificates-vs-server-certificates
  - https://www.jscape.com/blog/client-certificate-authentication
  - https://www.ssl2buy.com/wiki/what-is-the-difference-between-client-and-server-certificates
  - https://medium.com/@sevcsik/authentication-using-https-client-certificates-3c9d270e8326
  - https://blogs.msdn.microsoft.com/kaushal/2015/05/27/client-certificate-authentication-part-1/
- Keytool
  - view jks
- JKS
  - https://self-learning-java-tutorial.blogspot.co.uk/2015/07/extract-private-and-public-key-from.html
  - https://self-learning-java-tutorial.blogspot.co.uk/2015/07/extract-private-public-key-from-keystore.html
- Perm
- cert
  - https://www.jscape.com/blog/an-overview-of-how-digital-certificates-work
  - https://www.instantssl.com/articles/why-a-client-ssl-certificate-may-be-a-good-idea.php
- openssl
  - view certs
- tls
- Https
  - ssl
  - certificates and keys
- software(???)
- key pass app to store passwords
- create random passwords on the fly

## Secrets

- Encryption
  - base64 encoding
    - https://self-learning-java-tutorial.blogspot.co.uk/2018/02/convert-certificate-into-base64-encoded.html
- Decryption
- asc
- What to encrypt
  - passwords (database)
  - keys (tls)

## GDPR

- data deletion
  - scheduled
## Authentication and Authorisation

- https://serverfault.com/questions/57077/what-is-the-difference-between-authentication-and-authorization

## Encryption

## types

- Communicating with the application
  - Use of HTTPS, necessary certificates
  - Use of authentication and autherisation, must be logged in and have correct access rights to
    - access app or parts of apps
    - start, stop, restart app/pods
    - view properites, change them
- Access to database
  - Use of authentication and autherisation, must be logged in and have correct access rights to read or read/write in different environments
- How app communicates with 3rd party apps
  - certificates, authentication, https
- Log users who access app
