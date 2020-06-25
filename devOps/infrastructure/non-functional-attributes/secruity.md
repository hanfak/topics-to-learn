# Secruity

- Definition
  - information systems security can be defined as the combination of availability, confidentiality, and integrity, focused on the recognition and resistance of attacks.
  - Computer crimes use some form of gaining control over IT infrastructures
  - Preventing information being leaked or changed, preventing actions that system will take from doing something unwanted, preventing application from not working or working below standards
- Reasons for commiting coputer crimes
  - Personal exposure and prestige
  - Creating damage
    - create bad publicity for company
    - defacing websites, bringing down systems or websites, or making internal documents public.
  - Financial gain.
    - by holding data hostage and asking for ransom, stealing credit card data, changing account data in bank systems, or stealing passwords of customers and ordering goods on their behalf.
  - Terrorism
    - creating fear and chaos in a society
    - controlling water supply or nuclear plants
  - Warfare
    - Hacking over country's systems for intel or damage

## Risk Management

- Managing security is all about managing risks.
  - If there are no risks, we don't need any security controls.
- The effort we put in securing the infrastructure should therefore be directly related to the risk at hand
- Definition
  - Risk management is the process of
    - determining an acceptable level of risk
    - assessing the current level of risk
    - taking steps to reduce risk to the acceptable level
    - maintaining that level.
- A risk list can be used to quantify risks
  - Created with help of stakeholders
  - Definesthe following
    - asset: the component that needs to be protected.
    - vulnerability: a weakness, process or physical exposure that makes the asset susceptible to exploits
    - exploit: a way to use one or more vulnerabilities to attack an asset
    - probability: an estimation of the likelihood of the occurrence of an exploit (how often do we estimate this will happen)
    - Impact: he severity of the damage when the vulnerability is exploited.
    - Risk: The probablity x impact
- Controls mitigate these risks.
  - Example: a control for the risk of laptops with sensitive data getting stolen is to encrypt the hard disk to make the data unreadable for anyone but the owner.
  - Controls can be designed and implemented based on the identified severity of the risk in the risk list.

### Risk Response

- Definition
  - An agreed upon response to each risk decided by senior management
- Types of risk
  - Acceptance of risk
    - the risk could be accepted if the risk is very unlikely to happen and the costs of the damage imposed by exploitation of the risk is low and the cost of mitigating the risk is high.
  - Avoidance of risk
    - do not perform actions that impose risk
    - for instance, don’t host your own website or e-mail server
  - Transfer of risk
    - transfer the risk to an insurance company, if it happens, the insurance company will pay for the damage
  - Mitgation of risk and accepting the residual risk
    - How
      - Design for minimum risk
        - Design the system to eliminate as much vulnerabilities as possible.
        - Example
          - Using source code analysis in software development
          - by running critical systems stand-alone instead of connected to other systems
      - Incorporate safety devices
        - Reduce risk using devices like firewalls and hardened screened routers.
        - Dont affect the probabilty of exploit occuring, but reduces severity of the exploit
          - ie automobile seat belt doesn’t prevent a collision,
          - ie firewall oes not prevent attacks, but reduces the chance of an attacker connecting to sensitive parts of the network.
      - Provide warning devices
        - used to detect an undesirable condition, and to alert staff, or take automated actions.
        - Intrusion Detection System that alerts systems managers when a system is under attack
      - Implement training and procedures.

### Exploits

- Types of explouting a system
  - Key loggers can be maliciously installed on end user devices.
    - They can send sensitive information like passwords to third parties.
    - Someone needs to install it on the box either physically or via ssh/network using authenticated access
  - Network sniffers can show network packages that contain sensitive information or replay a logon sequence by which a hacker can successfully authenticate to an IT system.
    - wireshark
    - man in the middle attack
    - Use of https & tls to encrypt data over the wire
  - Data on backup tapes outside of the building can get into wrong hands.
    - Or extracting data via portable device (ie usb stick)
    - PCs or disks that are disposed of can get into the wrong hands
    - End users are led to a malicious website that steals information
      - phishing
    - Use of access logs, to show actions of all users
    - some alerting for certain actions

### Secruity controls

- Three goals of secruity (CIA)
  - Confidentiality
    - prevents the intentional or unintentional unauthorized disclosure of data.
    - Examples of levels
        - 1 = Public information
        - 2 = Information for internal use only
        - 3 = for internal use by restricted groups
        - 4 = secret, reputationla damage if leaked to public
        - 5 = top secret, damage to organisation ro society if leaked
  - Integrity
    - Ensures
      - No modifications to data are made by unauthorized staff or processes.
      - Unauthorized modifications to data are not made by authorized staff or processes.
      - Data is consistent
    - Examples of levels
      - 1 = integrity is of no importnance
      - 2 = errors in info are allowed
      - 3 = only incidental erros in information are allowed
      - 4 = no errors allowed, leads to reputational damage
      - 5 = no errors allowed, leads to society damage
  - Availability of information
    - ensures the reliable and timely access to data or IT resources by the appropriate staff
    - Examples of levels
      - 1 = no requirements on availability
      - 2 = some unavailability is allowed during office hours
      - 3 = some unavailability is allowed outside office hours
      - 4 = no unavailability is allowed risk to company damage
      - 5 = no unavailability is allowed risk to society damage
- For all applications and data set, a CIA classification should be given
  - using the levels above
  - Once levels given,then controls can be implemented to mitigate the identified risks
  - Auditors can see how risk is controlled
  - project manages can calculate effort needed to make system secrure


### Attack vectors

- Attacks on the infrastructure can be executed using
  - malicious code
    - are applications that, when activated, can cause network and server overload, steal data and passwords, or erase data.
    - Types
      - Worms
        - are self-replicating programs that spread from one computer to another, leaving infections as they travel.
      - A virus
        - is a self-replicating program fragment that attaches itself to a program or file enabling it to spread from one computer to another, leaving infections as it travels
      - Trojan Horse
        - Some software that appears to be useful software but will actually do damage once installed or run on your computer
        - Users are usually tricked into starting them because they appear to be receiving legitimate software or files from a legitimate source. Trojan horses can be used to deliver viruses or worms.
    - Most malicious code can be detected and removed by virus scanners.
      - Detecting viruses is mostly done using a so-called virus signature– a unique string of bits that identifies a part of the virus. When a file contains this signature, it is assumed that the file is infected with the viral code.
      - Heuristic scanning looks for certain instructions or commands within a program or script that are not found in typical applications
  - denial of service attacks
    - A Denial of Service (DoS) attack is an attempt to overload an infrastructure to cause disruption of a service
    - his overload can lead to downtime of a system, disabling an organization to do its business.
    - How
      - an attacker fires off a large number of (often malformed) requests to a server reachable from the internet
      - Because of the high load the server needs to process, or because the requests fill up the request queues, the server either crashes, or performs so slow that in effect it is not functioning anymore.
    - Distributed Denial of Service (DDoS) attack is used, as more than one server is used and cannot be brought down using dos attakcs
    - can use groups of computers that are infected by malicious code, called botnets, to perform an attack.
    - To prevent
      - Split business and public resources so that in case of an attack the business processes are not effected
      - Move all public facing resources to an external cloud provider
      - Setup automatic scalability (auto scaling, auto deployment) using virtualization and cloud technology
      - Limit bandwidth for certain traffic – for instance limit the bandwidth or the maximum number of calls per second on ports 53 (DNS)
        - as increased spike in traffic is a sign of dos
      - Lower the Time to Live (TTL) of the DNS records to be able to reroute traffic to other servers when an attack occurs
      - Setup monitoring for early detection on:
        - Traffic volume
        - Source and number of requests
        - Transaction latency
    - When it occurs:
      - Immediately inform your internet provider and ask for help
      - Run a script to terminate all connections coming from the same source IP address if the number of connections is larger than ten
      - Change to an alternative server with another IP address
      - Scale-out the public facing environment under attack
      - Reroute or drop suspected traffic
    - Use of CDN can be used to route traffic to your website
    -
  - social engineering
    - social skills are used to manipulate people to obtain information, such as passwords or other sensitive information, which can be used in an attack.
    - Use of cognitive biases
  - phishing
    - a technique of obtaining sensitive information.
    - Typically, the phisher sends an e-mail that appears to come from a legitimate source, like a bank, requesting "verification" of information.
      - The e-mail usually contains a link to a fraudulent web page that seems legitimate, with a form that captures your sensitve data like passwords, pins etc
  - Baiting
    - uses physical media, like an USB flash drive, and relies on the curiosity of people to find out what is on it.
    - The media is infected
    - Turn off auto run

## Secruity Patterns

### Identity and Access Management (IAM)

- the process of managing the identity of people and systems, and their permissions
- STeps
  - Users or systems claim who they are:
    - identification – they provide their identity, typically their name.
  - The claimed identity is checked:
    - authentication – identities provide for instance a password, which is checked
  - Permissions are granted related to the identity and the groups it belongs to:
    - authorization – identities are allowed into the system
- Connecting identities and their permissions
  - ie the kernel of an operating system owns an administration of users and a list of user rights that describes which identities are allowed to read, write, modify, or delete files. Trusted Computing Base (TCB)
- USed in apps, database and systems
- Single Sign-On (SSO), a user logs in once and is passed seamlessly, without an authentication prompt, to SSO enabled applications.
  - risk when the login credentials of a user are known, an attacker gains access to all SSO enabled systems for that user.
  - SSO is typically implemented using identity providing systems like LDAP, Kerberos, or Microsoft Active Directory.
  - Users authenticate to these identity providers, and applications trust the identity provider, so they allow access when a user is authenticated
  - Federated identity management extends SSO above the enterprise level, creating a trusted identity provider across organizations.
    - participating organizations share identity attributes based on agreed-upon standards, facilitating authentication from other members of the federation and granting appropriate access to systems
- users can be authenticated in one of three ways:
  - Something you know, like a password or PIN
    - Many systems only use a username/password combination
  - Something you have, like a bank card, a token or a smartphone
  - Something you are, like a fingerprint or an iris scan
  - systems use multi-factor authentication, where at least two types of authentication are required
    - n ATM machine, where both a bank card is needed (something you have) and a PIN (something you know)
- Role Based Access Control (RBAC) model
  -  identities are members of one or more groups (typically related to their roles in the organization) and, instead of granting permissions to individual identities, groups are granted permissions. And since groups can be nested (a group is member of another group)

### Segregation of duties and least privilege

- Also known as separation of duties
  - assigns related sensitive tasks to different people or departments.
  - The reasoning is that if no single person has total control of the system’s security mechanisms, no single person can compromise the system
  - ie Vault, cannot access system as root unless x number keys are used
- principle of least privilege.
  - that users of a system should have the lowest level of privileges necessary to perform their work, and should only have them for the shortest length of time.
- In many organizations, a systems manager has full control of the system’s administration and security functions.
  - bad idea
  - Security tasks should not automatically be given to the systems manager.
  - In secure systems, multiple distinct administrative roles should be configured, like a security manager, a systems manager, and a super user.
    - The security manager, systems manager, and super user may not necessarily be different people (but this would be preferred of course).
    - these roles are controlled, logged, and audited
  - a two-man control policy can be applied, in which two systems managers must review and approve each other’s work.
    -  minimize fraud or mistakes in highly sensitive or high-risk transactions.

### Layered Security

- also known as a Defense-In-Depth strategy
- to implement security measures in various parts of the IT infrastructure
  - comparable with physical security
    - place as many different barriers to cross
    - each barrier requires differetn skills
    - Increase time to break down barriers, increase risk of detection
    - Number of barriers should be unknown (or changing)
    - All barriers are independet, when one is crossed the others remain intact or if it has a vulnerability
- Each layer can be integrated with an Intrusion Detection System
- A disadvantage of implementing layered security is that it increases the complexity of the system.
- Every security layer must be managed, and systems managers must have knowledge about all used technologies
  - a risk if they are compromised

### Cryptography

- the practice of hiding information using encryption and decryption techniques.
- Encryption is the conversion of information from a readable state to apparent random data.
  - Only the receiver has the ability to decrypt this data, transforming it back to the original information
- A cipher is a pair of algorithms that implements the encryption and decryption process.
  - The operation of a cipher is controlled by a key.
  - The key is a secret onlyknown by the sender and receiver
  - Two types of ciphers:
    - block ciphers
      - takes as input a block of plaintext and a key, and outputs a block of cipher text.
      - popular ones The Data Encryption Standard (DES) and the Advanced Encryption Standard (AES)
        - DES is deprecated, more secure is triple DES
      - uses
        - ATM machine data encryption to e-mail privacy and secure remote access
    - stream ciphers
      - create an arbitrarily long stream of key material, which is combined with the plaintext bit-by-bit or character-by-character.
      - used when data is in transit using a network
      - the output stream is created based on a hidden internal state which changes as the cipher operates. That internal state is initially set up using a secret key. RC4 is a widelyused stream cipher.

#### Symmetric key encryption

- Symmetric key encryption is an encryption method where both the sender and
receiver share the same key.
- example
  - X sends a file to Y and encrypts it before sending using a cipher and a secret shared key. Upon receiving the file, Y’s cipher decrypts the data stream using the same key, leading to the original file. Both ciphers use the same secret shared key, only known by X and Y
- disadvantage
  - the key management necessary to use them securely. Each pair of communicating parties must share a different key.
  - The number of keys increases exponentially with number of users
  - The difficulty of securely establishing a secret key between two communicating parties, when a secure channel does not already exist between them, also presents a chicken-and-egg problem.

#### Asymmetric key encryption

- two different but mathematically related keys are used: a public key and a private key.
- The public key may be freely distributed and is for instance published on the organization’s website. Its paired private key must remain secret by the organization
- Example
  - X sends a file to Y and encrypts it before sending using a cipher and Y’s public key. The encrypted file can only be decrypted using Y’s private key (which must be kept a secret to everyone but Y). Upon receiving the file, Y’s cipher decrypts the data using his private key, leading to the original file.
  - When Y wants to send a file to X, X’s public and private keys are used
- disadvantage
  - very slow process
    - it is mostly used to setup a channel between two parties, to safely exchange a new, temporary symmetric key,
    - After exchanging symmetric keys, the rest of the communication is done using much faster symmetric key encryption.
- Commona algorithms
  - Diffie–Hellman and RSA algorithms

#### Hash functions and digital signatures

- Hash functions take some piece of data, and output a short, fixed length text string (the hash) that is unique for that piece of data and which can be used to validate the integrity of the data
  - practically impossible to find two pieces of data that produce the same hash
  - If the hash of a piece of data is known, and the hash is recalculated later and it matches the original hash, the data must be unaltered
- The length of this hash will not grow, even if the input for the hash function is increases
- Popular hash functions
  - MD5, SHA1 and SHA512
- To create a digital signature, a hash is created of some text (like an e-mail) and encrypted with the private key of the sender
  - The receiver decrypts the hash key using the sender's public key.
  - The receiver also calculates the hash of the text and compares it with the decrypted hash to ensure the text wasn't tampered with
  - Since the hash was encrypted using a private key, it is guaranteed that the hash was created by the owner of the private key
- Used
  - network security schemes (like SSL/TLS and many VPNs

#### Cryptographic attacks

- It is scientifically proven that a so-called one-time pad cipher is unbreakable, provided the key material is truly random, never reused, kept secret from all possible attackers, and of equal or greater length than the message.
  - Very impractical
  - as the key must be exchanged between sender and receiver in a safe way, and the key has the same length as the data to be transferred. So, you might as well exchange the data in a safe way instead of the key.
- brute force attack
  - Most ciphers, apart from the one-time pad, can be broken given enough computational effort
  -  consists of systematically checking all possible keys until the correct key is found.
  - The amount of effort needed, however, is usually exponentially dependent on the size of the key
- **Effective security could be achieved if it is proven that no efficient method (as opposed to the time consuming brute force method) can be found to break the cipher.**
- Most successful attacks are based on flaws in the implementation of an encryption cipher.
- You should not do create own chipher
  - use open source ciphers 
