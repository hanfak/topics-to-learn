# Secruity

## Certificates

- Keytool
- JKS
- Perm
- cert
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
- Decryption
- asc
- What to encrypt
  - passwords (database)
  - keys (tls)

## GDPR

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
