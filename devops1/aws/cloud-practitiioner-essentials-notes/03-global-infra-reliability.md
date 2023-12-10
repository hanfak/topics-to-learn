# Module 3 Global Infrastructure and Reliability

- Handling availability and fault tolerance
  - Multiple regions where data centers
  
## Global Infrastructure

- You have the choice of selecting the region your app is stored and operate in
- Can run in other data centers in different places
  - Having one building it is single point of failure
- Prevent issues with loss of connection to that data center
  - Have second data center - but costs a lot
  - Store back ups, but slow to bring back up
- Inside each region (all over the world) have multiple data centers 
  - each region is connected (fttp)
  - Each region is isolated, and secured using your own configuration
    - ie no data must leave that region unless you set it to
- choice region, allows having app closer to consumer
- Decision in choosing the region:
  - Compliance: does it meet the laws? Do I have to run it that region to access those customers
  - Proximity: closer to customer the faster it gets to the clients
  - feature availablity: Not regions have all features you want
  - pricing: Different regions costs more
- Availability zone 
  - a single data center or a group of data centers within a Region
  - Not built next to each other (ie same building)
    - located tens of miles apart from each other.
    - Have low latency and isolation if disater hits an AZ
  - Best practice, to run across at least two AZ in a region
    - Have 2 EC2 instances in a scaling group, but placed in different AZ in the region

## Edge Locations 

- CDN
-  site that Amazon CloudFront uses to store cached copies of your content closer to your customers for faster delivery.
- Handles serving customers not close to a region
- Instead of moving data to a new region, can use a copy/cache from a region further away,
- Provides low latency, high transfer speed
- Issues with stale or inconsistent data, when to expire cache
- Seperate from regions
- Run DNS (Route 53) also
- AWS Outpost
  - create an amazon datacenter in the your building, run by amazon but isolated to your building
  - 
## How to Provision AWS Resources

- Everything AWS is an API call to provision, configure, and manage your AWS resources.
- AWS Management Console
  - GUI
  - includes wizards and automated workflows
  - AWS Console mobile application to perform tasks such as monitoring resources, viewing alarms, and accessing billing information
- AWS Command Line Interface (AWS CLI)
  -  control multiple AWS services directly from the command line on multiple OS
  -  automate the actions that your services and applications perform through scripts
- software development kits (SDKs)
  - SDKs enable you to use AWS services with your existing applications or create entirely new applications that will run on AWS.

### AWS Elastic Beanstalk

- provide code and configuration settings, and Elastic Beanstalk deploys the resources necessary to perform the following tasks:
  - Adjust capacity
  - Load balancing
  - Automatic scaling
  - Application health monitoring

### AWS Cloud Formation
-  treat your infrastructure as code 
  - declarative
- build an environment by writing lines of code instead of using the AWS Management Console 
- provisions your resources in a safe, repeatable manner
- It determines the right operations to perform when managing your stack and rolls back changes automatically if it detects errors.


## Links 

- https://aws.amazon.com/about-aws/global-infrastructure/
- https://aws.amazon.com/about-aws/global-infrastructure/regions_az
- https://aws.amazon.com/blogs/networking-and-content-delivery/
- https://aws.amazon.com/tools/
- https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23content-delivery
