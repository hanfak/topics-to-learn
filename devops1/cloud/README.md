# Cloud computing

## What

- In cloud computing, the capital investment in building and maintaining data centers is replaced by consuming IT resources as an elastic, utility-like service from a cloud “provider” (including storage, computing, networking, data processing and analytics, application development, machine learning, and even fully managed services).
- The practice of using a network of remote servers hosted on the internet to store, manage and process data, rather than a local server or personal computer

## Advantages

- improve flexibility, reduce costs, and focus on core competencies, but also to fully transform how they operate
  - by re-designing internal workflows or customer interactions as digital experiences that extend from the data center all the way through to mobile devices.
- Resources can be purchased and consumed on a “pay-as-you-go” basis, and increased or decreased as needed for optimal utilization.
- Capital expenses can be converted into operating expenses.
- Cloud customers can focus on rapid innovation without the expense and complexities of hardware procurement and infrastructure management.
- End-user productivity is likely enhanced because no software is installed, configured, or upgraded on personal devices, and services can be accessed from anywhere.
- Infrastructure functionality, performance, reliability, and security are likely to improve because customers can benefit from “vertically integrated” stacks that are customized at every level — which would be out of reach for on-premises deployments built from off-the-shelf components.
- helping customers forget about the existence of that infrastructure entirely (aka “serverless” computing), thereby freeing them to unlock full digital business transformation.
- You are responsible for your configuration of the cloud services and code and someone else handles the rest
- Trade capital expense for capital expense
  - No upfront costs
    - instead of paying for servers or data centers
  - Pay on demand
    - pay only when you consume compute resource
- Benefit from massive economies of scale
  - Usage from lots of customers, which lowers the cost
- Stop guessing capacity
  - elimintates guess work for infrastructure requirements
  - instead of paying for idle or under utilized servers, you can scale up or down to meet the current need
- Increase speed and agility
  - Launch resources very fast instead of waiting for it to be done manually and/or get permission when done on prem
- Stop spending money on running and maintiaing data centers
- Go global in minutes
  - deploy  very fast, and to local regions with low latency

## Use case for migrating to the cloud

- Disaster recovery (DR): maintaining data center redundancy can be expensive. Instead, storing redundant data in the public cloud, coupled with the use of specialized tools for managing the DR process, can be more cost-effective.
- Development & testing environments: similarly, using public-cloud infrastructure in lieu of replicating on-premises resources for test/dev can make significant capital investments unnecessary.
- Managed services: Collaboration apps, data analytics, and even machine learning can now be consumed as services that complement on-premises systems before making a wholesale infrastructure shift to the cloud.
- Data archiving: the public cloud can provide data storage at massive scale and cost-effectively.
- Specialized compute-intensive workloads: When access to massive computing power is needed but only on a transient/ad-hoc basis, the cloud is an efficient option.

## Providers

- Azure, AWS, Google cloud
- Internal Clouds, private clouds for the company

## Types

- SAAS
  - for customer
  - A completed service/product that is run and managed by the service provider
    - it just works, maintaince is not worry
    - ie gmail, office 360
- PaaS
  - for developers
  - Removes the need for oyour organisation to manage the underlying infrastructure, and focus on the deployment and management of your services
    - dont worry about OS, provisioning, configuring, or understanding the hardware
  - ie Horeku, beanstalk
- IaaS
  - for the admins (SA)
  - Building blocks of cloud computing
  - provides access to networking features, computers and data storage space
  - Dont worry about IT staff, data centers, or hardware
  - ie Azure, AWS, Google cloud

## Deployment models

- Cloud
  - fully utilising cloud
  - users
    - startups
    - SaaS offerings
    - new projects and companies
- Hybrid
  - use of both cloud and on premises
  - users
    - banks, fintech
    - large professional services
    - legacy on prem
- On premise
