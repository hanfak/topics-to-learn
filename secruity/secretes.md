# Secrets

## what

- These are properties that should only be known by a select few authorised users, who need it for a specific purpose
  - Examples
    - applications
    - services
    - privileged accounts
    - other sensitive parts of the IT ecosystem.
- Examples of types of secrest
  - Database passwords, users, urls
    - and other system-to-system passwords.
  - urls for specific end points
    - API and other application keys/credentials
  - tls private keys (server and client)
  - user access to applications usernames and passwords
  - tokens
  - User or auto-generated passwords
  - Private encryption keys for systems like PGP
  - RSA and other one-time password devices
- Some secrets are needed at startup, ie at time of deployment.
  - Others are needed at time of usage while the application is up. This can allow the app to access a secret managemnet tool to get the secret and this is only accessible in the secret managemnet tool
- Used for authenticating applications and users and providing them with access to sensitive systems, services, and information
- Secrets are normally encrypted, especially if stored anywhere where people can gain access, ie git repo, or transferred
  - Because secrets have to be transmitted securely, secrets management must account for and mitigate the risks to these secrets, both in transit and at rest.
- Secrets can also be managed by a secrets management tool, like vault

## Secrets in clusters

- when deploying an app which has some secrets, the secret is encrypted using a public key and stored in a property file.
  - Then when deployed, the kluster or some hidden proxy will decrypt it (using the private key which is linked to the public key that encrypted it - aysemetric encryption) and store it in the kluster, which is passed to the application to use.
  - No one or only a select few should have access to view the secret in the cluster, as it is now decrypted. And those that do, there should be an audit trail of who has accessed this secret.
  - The private key is also hidden, as this can be used to decrypt the encrypted secret

### Rotation of encryption keys

- When using encryption, we should always be rotating the public and private keys
  - So if there is a leak of the private key, then this is mitagate
  - https://security.stackexchange.com/questions/198324/rotating-encryption-keys-how-does-it-work
- a key rotation is represented by generating a new key version of a key, and marking that version as the primary version.
- Rotating a key doesn't disable or destroy previous key versions. The previous key versions will no longer be primary, but they remain available for decrypting data.
- Why
  - to reduce the amount of content encrypted with that key so that the amount of material leaked by a single key compromise is less.
  - for signing keys there is a concrete reason: say it takes 𝑋 months of computation (expected value given your threat model) to crack a key, and you rotate your signing key every 𝑋−1 months and revoke the old one, then by the time an attacker has cracked the key, any new signatures produced by the attacker will either be A) rejected by clients because of key expiry, or B) back-dated to before the key revocation (which should also raise warning in clients).
  - To limit the number of encrypted messages available to cryptanalysis for a specific key version.
  - To ensure your system is prepared in the event you need to rotate to a stronger algorithm.
    - otherwise a system tends to become dependent on specific keys, which makes it very difficult to initiate key rotation after an incident.
    - The first time you try key rotation should not be during real-time recovery from an incident.
  - To reduce the volume of ciphertext that would be unprotected if a key version is compromised.
  - To prevent use of a key version that is compromised or suspected of being compromised
- Frequencey of rotation
  - Regular rotation:
    - Regularly rotate the encryption key used, limiting the amount of data protected by a single key.
    - Regular rotation may be required for internal business compliance.
  - Irregular rotation:
    - Ad-hoc rotation after a suspected incident, as an additional stopgap.
    - Data encrypted with the previous version of the key may also need to be re-encrypted.
  - disablement schedule:
    - to re-encrypt older data and disable keys after a certain time period, e.g., 20 key versions enabled for up to 5 years of data.
- Automated rotation
  - a way to change rotation of keys in an automated way. Normally done via applications like vault.

## Secret Management
