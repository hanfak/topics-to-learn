# Security

## AWS Shared Responsibility Model

- All resources are secured by both customer and AWS
- AWS env is not a single object
  - a Collection of parts built on top of each other
  - Some parts AWS is responsible for, and others the customer is
- Two parts 
  - customer responsibilities aka security in the cloud
    - responsible to secure everything that is created and put in aws
    - customer of aws has complete control over content
    - Layers
      - client side data, server side encryption; network traffic protection
      - os, network, firewall config
      - platform, app, iam
      - customer data
  - AWS responsibilities aka security of the cloud
    - responsible of construction and ensuring it is solidly built
    - Handles the layers of infrastructure
    - aws provides reports from 3rd party audtiors
    - Layers
      - regions, az, edge locations
      - hardawar, global infrastructure
      - compute, storage, database, networking
      - software

## User Permissions and Access (AWS Identity and Access Management (IAM))

- managess access to AWS services and resources securely
- When new AWS account created, a **AWS account root user** is created
  - Has permissions for everything (create users, access all data and resources). very powerful
  - Should have MFA turned on 
  - Should not use root user for everyday tasks
    - Should create another user with less privileges (permissions). 
    - should create a user which can create other users
    - Only use it root for very specific tasks
      - ie changin account settings (account name, email address, root user password, and root user access keys)
      - changing support plan
      - Restore IAM user permissions
      - View certain tax invoices
      - Close AWS account
      - for others see https://docs.aws.amazon.com/IAM/latest/UserGuide/root-user-tasks.html

### IAM Users

- An identity created in AWS
- represents a person or app that interacts with service or resource
- HAs 
  - name 
  - credentials
- Default on creatoin has no permissions
  - Need to grant permissions
- Always create a new user for each person using it

### IAM Policy

- document that allows or denies permissions to AWS services and resources
- Assign a policy to a user or group
- Customise users levels of access to resources
- Should follow priniciple of least privilege for granting permisssions
  - Have the least number of permissiosn to perform their task
  - dont grant access to all buckets, when one is all that is needed
- Example 
  ```json
  tbc..

  ```
  - parts
    - Version
      - of the policy, different versions have different features
    - Statement
      - effect
        - either Allow or Deny
      - action
        - The action that the effect will have on, ie s3:listObject
      - resources
        - references the specific id of the resource

### IAM groups

- A collection of IAM users
- When policy is assigned, then all users of the group are granted those policies defined in the policy

### IAM Roles

- An identity that you can asssume to gain temp access to persmissions
- IAM user, app or service must be granted permissions to switch roles before assuming a Role
- On assuming a role, they lose all previous permissions under previous role

### MFA

### Links 

- https://docs.aws.amazon.com/iam/

## AWS Organisations

- Consolidating multiple AWS accounts in central location
- Good for growth of company
- A root is created on creation
- centrally control permissions for all accounts in the organisation
  - use service control policies (SCP)
  - place restrictions on AWS servies and individual api actions
  - consolidated billing

### ORganisational Units

- Organise accounts in groups
- manage accounts with similar business and security requirements

## Compliance (AWS Artifact)

- There are specific standards that must be followed
  - These will be checked to ensure they are upheld via auditing or inspection from internal and external parties
  - Not doing so can lead to fines, prison, loss of contract, loss of reputation etc
  - Ie taxes, gdpr
- Aws provides tools to collect documents, records and insepct env to see if it meets compliance regulations
- AWS already builds all the infrastructure using best practices, which you inherit
  - Following specific compliance rules see https://aws.amazon.com/compliance/programs/
  - Depending on the region you use, it will already be compliance ready for that region
    - ie data will not be replicated into a different region if stored in a specific region
  - You own your data 
    - Which you can encrypt in ways that best suit you
  - You can ask AWS to provide documents to show they are following the compliance 
    - Can be found *AWS artifact*
      - Can select online agreements
    - Third party reports on compliance met by AWS -> see *AWS Compliance*
  - Due shared responsibility model, the stuff you build needs to have it's complaince done by you
- AWS Artifact has two sections
  - AWS Artifact Agreements
    - can review, accept, and manage agreements for an individual account and for all your accounts in AWS Organizations.
  -  AWS Artifact Reports
    -  provide compliance reports from third-party auditors.
- Customer Compliance Center
  - contains resources to help you learn more about AWS compliance. 
  - access compliance whitepapers and documentation on topics 
  -  includes an auditor learning path.

## Denial of service (DoS) attacks

- Attack on your system 
- How carried out
  - Shut down app to function, by overwhelming the capacity of the app with mutliple requests, so that no one else can access it (ie real customers)
  - One computer/actor doing this will not provide enough requests to overwhlem service, instead DDoS (distrubuted) is used
    - Leverages other machines (their or unknowningly hacked machines)
    - This allows for random ip addresses to hit the service
    - The main bot, will do little and delegate the majority of the work to the zombie bots
  - Example
    - UDP Flood ie weather info is sent to your service, by malicious actor settign the response address to victim host
    - Http level attacks, lots of (fake) users requesting stuff from the service
    - Slowloris attack, the attack pretends to have a slow connection, so holds up the server
- How to defend
  - Use security groups
    - to only allow specific traffic (ie hosts, type of connections)
  - ELB will handle slow connections
  - AWS Shield with AWS WAF
    - standard service 
      - no costs
      - USes analysis techniques to detect malicious traffic
    - Advnaced 
      - paid
      - provides detailed attack diagnostics 
      - detect more sophisticated ddos
      - Integrates with ELB, route 53, cloudfront

## Additional Security Services 

- Encryption
  - securing a message or data in a way that can only be accessed by authorized parties
  - encryption at rest
    - data not moving
    - all data in dynamo db is encrypted
  - encryption in transit
    - data travelling between servies
    - use SSL and certificates
  - Integrated with AWS key management service (KMS)
  -  AWS key management service (KMS)
    - perform encryption operations through the use of cryptograhic keys
    - cryptographic keys
      - random string of digits used for locking(encypting) and unlocking (decrypting) data
    - manage, create and use keys, control use of keys
    - Can specify IAM users and roles that can manage keys
    - Can disable keys (perm/temp)
    - keys never leave KMS
- AWS WAF
  - Web application firewall
  - monitor network requests that enter apps
  - works with cloudfront and ELB
  - uses the web access control list (ACL) to block or allow traffic
- amazon inspector
  - perform automated security assessments
  - Checks for security vulnerabilities and deviations from best practices
  - ie open access to EC2 or installations of vulnerable software versions
  - Provides a list of findings (gui) with serverity levels
- amazon guardduty
  - intelligent threat detection
  - identifies threats from monitoring network activity and behaviour
  - uses multiple sources like vpc logs and dns logs
  - Can automate fixes using a lambda to act on specific problems
  - running outside of apps so no affect on performance

## Links 

- https://aws.amazon.com/products/security
- https://docs.aws.amazon.com/whitepapers/latest/introduction-aws-security/welcome.html
- https://docs.aws.amazon.com/whitepapers/latest/aws-overview-security-processes/aws-overview-security-processes.pdf
- https://aws.amazon.com/blogs/security/
- https://aws.amazon.com/compliance
- https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23security-identity-compliance
- https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html