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

## Compliance

