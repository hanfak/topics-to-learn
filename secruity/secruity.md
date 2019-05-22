# Secruity

## General

- https://www.javaworld.com/article/2075336/secure-your-java-apps-from-end-to-end--part-1.html#tk.rss_howtojava
- https://portal.securecodewarrior.com/#/learning-resources/
- https://medium.com/myheritage-engineering/10-tips-to-power-up-your-java-security-f3daa4522530
- https://www.owasp.org/index.php/Main_Page
- https://www.youtube.com/watch?v=Gnxk_uf6qTQ
- https://www.youtube.com/watch?v=zlEdzJccdps&list=WL&index=163&t=0s

## Certificates

- client cert
  - https://www.websecurity.symantec.com/security-topics/client-certificates-vs-server-certificates
  - https://www.jscape.com/blog/client-certificate-authentication
  - https://www.ssl2buy.com/wiki/what-is-the-difference-between-client-and-server-certificates
  - https://medium.com/@sevcsik/authentication-using-https-client-certificates-3c9d270e8326
  - https://blogs.msdn.microsoft.com/kaushal/2015/05/27/client-certificate-authentication-part-1/
- Server certificates
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
  - https://robertheaton.com/2014/03/27/how-does-https-actually-work/
  - https://howhttps.works/the-keys/
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
