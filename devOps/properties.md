# Properties/configuration

properties is file containing a set of key value mappings (in different formats ie json/yaml/properties) that are constants used in the app for specific environments (ie same keys but different values for different environments)

## Types of properties

- deployment
  - These are necessary to start the application up
    - ie java options, which env to deploy to
  - They can also be used as a precondition before startup.
    - if not set or are wrong, then application cannot startup (obvisouly should be done before it gets to deployment)
- startup
  - These are needed for the app to run, after being deployed.
  - If they are not there then the application cannot do it's tasks
  - ie database properties
- In life properties
  - These properties can be changed throughout the lifecycle/running of the application
  - ie 3rd party url, toggles, certificates
- Secrets
  - These are generally things like passwords, usernames, tokens, private keys
  - They need to be encrypted when saved or stored anywhere (ie db/git), but upon deployment or usage needs to be decrypted
    - Either by the devs or someone with clearance
  - Generally decrypted on the environment/server, so the application can use them to function
    - This means they should never be shown in logs (or at least obfuscated), accessed by some user via the application (ie endpoint)
  - These secrets will generally have self life where they become out of date and need to be replaced (ie encrypted and stored)
- Local properties
  - these are a file which is a combination of all the above.
  - Where the property file is used by the app when done on a local environment ie dev computer, minikube etc
    - They can also be used when running the build ie all the tests, or running a test, or running the app via the main method, or docker container
  - Secrets would not be encrypted, unless decryption happens in the app (but this is not a good idea as the decryption key would need to be in the app)

## Property manager

- applications which manage the properties
- Use during the phases of the application (deployment, startup and inlife)
- Do not need to go through whole software process, ie change code
  - They are dynamic changes
  - The application will have system to call or listen for changes in the the PM and apply them ie for inlife properties
- Non developers can change it
  - Secruity reasons ie changing production passwords/certs, should be done by as few people as possible
- Can have properties passed in at time of deployment
  - the deployment system ie kubernetes, will pass in the properties at deployment and startup
- drawback
  - Not versioned control, lack of audits on who did what and hard to roll back
    - although this can be implemented
  - Properties changed while the application is running, may be reverted on the deployment of a new version of the application and thus lost
    - Need to remember to add these to the permenant property file for future versions
    - although the dynamic property might have been short lived, and not needed permenantly
  - Another DSL to learn

## Secret Management

- Vault


## Other

- Can separate CI and CD
  - When CI is complete a binary/jar/image is versioned and produced
  - The CD is configured with the version of the app which is ready to be deployed
  - The CD can now deploy to different environments (with different properties settings) independently instead of deploying in a set order (ie CI->test -> stage -> prod)
  - So we can do a release/deployment to prod with just changes to inlife properties to a version already in prod


## Separating properties from app in different projects

- stop deploying full app and only properties

## Other

- Use of environment variables in properties ie local database url


## Links

- https://docs.oracle.com/javase/tutorial/essential/environment/properties.html
