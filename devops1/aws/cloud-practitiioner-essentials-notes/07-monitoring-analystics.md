# 7 Monitoring and Aanlytics

- Watch how things are going, use metrics and observing them to decide what to do
- Alert to things that could go wrong in system
- Gain insights into usage of system 
- Need visibility into the state of the system

## Amazon Cloudwatch

- Monitor applications and infrastructure in real time
- tracking and monitoring metrics 
- Metrics 
  - variables that are tied to your resources
- Can apply rules around metrics (ie when reach a number)
  - Can alert monitoring users (people or apps) to perform some action that will turn off the alert
  - Cloud watch alarm (The rules to trigger alarm and action in Cloudwatch)
    - Integrated with SNS, so a notification can be sent to another service to perform an action
- Dashboard 
  - a feature that allows a user to view the metrics in real time
  - auto refreshing
- Beneifts
  - access to metrics from all places in a central locations
  - visibility into your apps, infras and services 
  - system wide view  
  - Reduce MTTR (mean time to resolution) and improve TCO (total cost of ownership)
    - Frees up developers from fixing or spending time fixing issues and focus on features
    - Thus reducing costs and time
  - Drive insights and optimise apps and resources

## AWS CloudTrail

- Trust but verify 
- Everything is recorded (auditing)
- Auditing tool for recording api calls
  - everything in AWS is an api call
- Every request is recorded in cloud trail
- Save logs in secure S3 buckets 
- Includes 
  - api called
  - time of call
  - source ip address
  - how it was made
  - etc
- Events are updated in cloud trail withing 15minutes 
  - use of SNS/SQS or some streaming system like kafka
- Cloudtrail insights
  - optional
  - automatically detects anomalies in api activities

## AWS Trusted Advisor

- Automated advisors 
- evaluate your resources against the following pillars:
  - cost optimization 
  - performance 
  - security
  - fault tolerance 
  - service limits
- Some are free
- can see in console
  - shows three areas for each pillar
    - green: all good 
    - orange: cost optimization
    - red: action recommended now


## Links 

- https://aws.amazon.com/products/management-tools
- https://aws.amazon.com/products/management-tools/use-cases/monitoring-and-observability/
- https://aws.amazon.com/products/management-tools/use-cases/configuration-compliance-and-auditing/
- https://aws.amazon.com/blogs/mt/
- https://docs.aws.amazon.com/whitepapers/latest/aws-governance-at-scale/introduction.html