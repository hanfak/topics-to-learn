# 8 Pricing and Support

- careful about exhausting credit

## AWS Free Tier

- Types
  - Always free
    - sagemaker, comprehend medical, dynamnodb, sns, cognito
  - 12 months free
  - trials
- Examples 
  - lamdba: 1 mill free invocations per month
  - dynamodb: 25gb per month
  - S3: free for 12 months for up to 5GB standard storage 
  - lightsail: 1 month free trail of 750 hours usage 

## AWS pricing concepts 

- pay for what you use
  - no long term contracts or complex licensing 
- Pay less when you reserve
  - offer discount to reserved (contract) than on demand
- Pay less with volumen based discounts when use more
  - The per unit cost decreases with increased usaged
  - ie S3
- AWS Pricing Calculator 
  - Helps create estimates for use case of AWS
  - Create groups of esitmates for organisation
  - ie check which region/instance type is most cost efficient

## Billing Dashboard

- To pay your bill
- monitor usage
- analyse and control costs
- publish cost and usage reports
- create budgets
- purchase and manage plans

## Consolidated Billing 

- simplifies billing process
- share svaings accross accounts
- free feature
- Part of AWS Organisation
  - manages multiple AWS accounts from central location
- receive single bill for all accounts in the org
- track combined costs of all accounts
- Max accounts is 4, but increase 

## AWS Budgets

- Set custom bugets for usage, instance reservations and costs
- proactively notified if going near or over (ie email/sns)
- update 3 times a day

## AWS Cost Explorer

- visualise, understand and manage costs and usage over time 
- Has default report of cost and usuage for top 5 highest costs
  - Can apply filters and groupings
  - Can tag resources with tags

## AWS Support Plans

- All get the free Basic Support  
  - access to whitepapers, documentation, and support communities
  - Can contact AWS for billing questions and service limit increases
  - 24/7 support
  - trusted advisor (limited)
  - personal health dashboard
    - alerst and remediation guidance
- Other plans are pay by month and no long term contracts
- Developer support
  - paid 
  - includes basic
  - open unrestricted number of tech support cases
  - Best practice guidance
  - Client-side diagnostic tools
  - Building-block architecture support
    - guidance for how to use AWS offerings, features, and services together
    - help you to identify opportunities for combining specific services and features.
- Business support
  - Use-case guidance to identify AWS offerings, features, and services that can best support your specific needs
  - All AWS Trusted Advisor checks
  - Limited support for third-party software, such as common operating systems and application stack components
    - contact AWS Support for assistance with installing, configuring, and troubleshooting the operating system
- Enterprise On-Ramp Support
  - A pool of Technical Account Managers to provide proactive guidance and coordinate access to programs and AWS experts
  - A Cost Optimization workshop (one per year)
  - A Concierge support team for billing and account assistance
  - tools to monitor costs and performance through Trusted Advisor and Health API/Dashboard
  - Consultative review and architecture guidance (one per year)
  - Infrastructure Event Management support (one per year)
  - Support automation workflows
  - 30 minutes or less response time for business-critical issues
- Enterprise Support 
  - A designated Technical Account Manager to provide proactive guidance and coordinate access to programs and AWS experts
  -  Concierge support team for billing and account assistance
  - Operations Reviews and tools to monitor health
  - Training and Game Days to drive innovation
  - Tools to monitor costs and performance through Trusted Advisor and Health API/Dashboard
  - Consultative review and architecture guidance
  - Infrastructure Event Management support
  - Cost Optimization Workshop and tools
  - Support automation workflows 
  - 15 minutes or less response time for business-critical issues
- Technical Account Manager (TAM)
  - primary point of contact at AWS. 
  - For Enterprise and on ramp support

## AWS Marketplace

- Find, test and buy software that runs on AWS
- information on pricing options, available support, and reviews from other AWS customers.
-  explore software solutions by industry and use case

## Links 

- https://aws.amazon.com/pricing
- https://aws.amazon.com/free
- https://aws.amazon.com/aws-cost-management/
- https://d1.awsstatic.com/whitepapers/aws_pricing_overview.pdf
- https://d1.awsstatic.com/whitepapers/introduction-to-aws-cloud-economics-final.pdf
- https://aws.amazon.com/premiumsupport
- https://aws.amazon.com/premiumsupport/knowledge-center/