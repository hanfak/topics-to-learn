# Module 2 Compute in the cloud

- EC2 
  - Virtual servers that host your application
  - These VS are hosted on AWS servers in their datacenters and ready to go
    - There are several VS per server, a VS can be moved to other servers
    - Multitenancy -> Sharing underlying hardware between virtual machines 
    - The hypervisor manages the VS on the server, ie memory 
    - Each EC2 instance is unaware of other instances on the same server
  - Dont have to do this (ie on prem)
  - Request only required resources (mem/compute etc) and AWS will provision these for your app to use 
    - Can change these resources (servers that are used)
  - Pay for only what is used 
    - Not when stopped or terminated
  - Provision EC2 in minutes
  - Can configure multiple areas
    - OS - win or linus
    - memory
    - ram
    - cpu
  - You decide what is running on the instance
  - It is resizable
    - Vertical scaling
  - Control networking aspect of EC2
    - How accessible the instance is to private or public
- Parts of EC2 
  - Launch
    - launch an instance
    - Configure - OS, hardware, security settings of network traffic in/out
  - Connect
    - Your programs and applications have multiple different methods to connect directly to the instance and exchange data. Users can also connect to the instance by logging in and accessing the computer desktop.
  - Use
    - you can begin using it. You can run commands to install software, add storage, copy and organize files, and more.

## EC2 Instance Types

- Have varying degrees of memory, cpu, traffic to meet needs
- General purpose instances 
  - provide a balance of compute, memory, and networking resources
  - Exampels
    - application servers
    - gaming servers
    - backend servers for enterprise applications
    - small and medium databases
  - For apps that dont need any specific optimizations
- Compute optimized instances
  - for compute-bound applications that benefit from high-performance processors
  - used workloads such as web, application, and gaming servers.
  -  ideal for high-performance web servers, compute-intensive applications servers, and dedicated gaming servers.
  - batch processing workloads that require processing many transactions in a single group.
- Memory optimized instances
  -  deliver fast performance for workloads that process large datasets in memory.
  - workload that requires large amounts of data to be preloaded before running an application. 
  - High performance databse
  - performing real-time processing of a large amount of unstructured data.
- Accelerated computing instances
  - use hardware accelerators, or coprocessors, to perform some functions more efficiently than on CPU
  -  floating-point number calculations, graphics processing, and data pattern matching.
  - game streaming, app streaming
- Storage optimized instances
  -  for workloads that require high, sequential read and write access to large datasets on local storage.
  - distributed file systems, data warehousing applications, and high-frequency online transaction processing (OLTP) systems.
  -  input/output operations per second (IOPS) is a metric that measures the performance of a storage device.

## EC2 Pricing

- Types
  - On demand
    - per hour or per second
    - for getting started or testing applications
    - apps with unpredictable usage patterns
    - get baseline of average usage
    - not recommended for workloads that last a year or longer because these workloads can experience greater cost savings using Reserved Instances.
  - Savings plans
    - make an hourly spend commitment to an instance family and Region for a 1-year or 3-year term.
    - Any usage beyond the commitment is charged at regular On-Demand rates.
    - don't need to specify up front what EC2 instance type and size , OS, and tenancy to get a discount.
    - don't need to commit to a certain number of EC2 instances over a 1-year or 3-year term
    - don't include an EC2 capacity reservation option.
  - Reserved Instances
    - billing discount applied to the use of On-Demand Instances
    - Buy for a 1-year or 3-year term. You realize greater cost savings with the 3-year option.
    - At the end of the term, you are charged on demand rates
    - Standard
      - you know the EC2 instance type and size you need for your steady-state applications and in which AWS Region you plan to run them
      - Know 
        - Instance type and size
        - OS
        - Tenancy: Default tenancy or dedicated tenancy
        - specify an Availability Zone
    - Convertible
      -  run your EC2 instances in different Availability Zones or different instance types
      - Less discount due to more flexibility
  - Spot Instances
    - For workloads with flexible start and end times, or that can withstand interruptions
    -  Spot Instances use unused Amazon EC2 computing capacity
    - Only start, when resource is available
    - if capacity is no longer available or demand for Spot Instances increases, your instance may be interrupted.
      - Give you a 2 minute warning before interupting (to allow app to save state)
    - Greater savings off On demand
    - background processing job that can start and stop as needed
  - Dedicated Hosts
    - physical servers with Amazon EC2 instance capacity that is fully dedicated to your use.
    - No one shares tenancy of those hosts
    - More expensive
- AWS Cost Explorer to analyze your Amazon EC2 usage over the past 7, 30, or 60 days. 
  - provides recommednations

## Scaling EC2

- beginning with only the resources you need and designing your architecture to automatically respond to changing demand by scaling out or in.
- Most buisnesses deal with variable demand
  - must be able to handle this demand to avoid loss of business 
  - In past needed to predict max demand and buy hardware first, leading to unused resources at greater cost (utilisation is low). Or buy for average demand, lose business during high demand above average
- Horizontal scaling
- Amazon EC2 Auto Scaling
  - Handles the scaling automatically
  - add or remove Amazon EC2 instances in response to changing application demand.
  - Improves availability of app, by removing single point of failure
- Types:
  - Dynamic: responds to changing demand.
  - Predictive scaling automatically schedules the right number of Amazon EC2 instances based on predicted demand.
  - These can be used together
- Can set min instances 
  -  at all times, there must be at least one Amazon EC2 instance running.
- min capacity
  -  number of Amazon EC2 instances that launch immediately after you have created the Auto Scaling group
-  set the desired capacity 
  - Number of instances needed required
  - if not set, this is defaulted to min capacity
- max capacity
  -  scale out in response to increased demand, but only to a maximum
  - These are started when demand increases, and removed when demand decreases
    - or when dynamic/predictive rules are met 

## Directing traffic with Elastic Load Balancing

- An AWS service, a load balancer
  - a single point of contact for all incoming web traffic to your Auto Scaling group.
- automatically distributes incoming application traffic across multiple resources
- the requests spread across multiple resources that will handle them
  - even distribution of workload
-  no single instance has to carry the bulk of it. 
- ELB is regional
- Can be used for communication between EC2 instances (and handle increased/decreased instances in the scaling group)
- ELB has a routing table, clients access the IP/DNS of ELB and routes to the VIPs of the instances

## Messaging and Queueing

- Communication between internal components can lead to service failure if one component is down and cannot fulfil the the synchronous request (ie http)
- Remove this tight coupling and failure, can use messaging and reduce the coupling of the components
- Amazon Simple Notification Service (Amazon SNS) 
  - pub/sub
  - publishers publish to a topic, and subscribers subscribe to that topic. So when message is published to a topic, the subscriber will receive it
  - Can subscribe to one or many topics
  - Can unsubscribe when needed
- Amazon Simple Queue Service (Amazon SQS)
  - Message queue (FIFO)
  - send, store, and receive messages between software components, without losing messages or requiring other services to be available
  - A Sender sends messages to a queue, a consumer retrieves messages from the queue it is subscribed to, processes it and deletes the message off the queue
    - Can have settings that delete message off queue when it has received it

## Additional Compute Services

- Serverless (AWS Lambda)
  -  code runs on servers, but you do not need to provision or manage these servers
  - Different to EC2 as you need to provision instances, upload code then manage instances while app is running
  - Avoid maintaining servers, focus on code
  - flexibility to scale serverless applications automatically
  - pay only for the compute time that you consume. Charges apply only when your code is running
  - The lambda will trigger when needed
    - need to configure trigger (ie http request to endpoint)
- Containers
  - standard way to package your application's code and dependencies into a single object
  - Container orchestration services help you to deploy, manage, and scale your containerized applications
- Amazon Elastic Container Service (ECS)
  - highly scalable, high-performance container management system that enables you to run and scale containerized applications on AWS.
  - Supports Docker
  - use API calls to launch and stop Docker-enabled applications.
- Amazon Elastic Kubernetes Service (EKS)
  - fully managed service that you can use to run Kubernetes on AWS. 
- AWS Fargate
  -  serverless compute engine for containers
  - Works with ECS and EKS
  - manages your server infrastructure for you

## Links 

- https://aws.amazon.com/blogs/compute/
- https://aws.amazon.com/products/compute/
- https://docs.aws.amazon.com/whitepapers/latest/aws-overview/compute-services.html
- https://aws.amazon.com/getting-started/decision-guides/modern-apps-strategy-on-aws-how-to-choose/
- https://docs.aws.amazon.com/savingsplans/latest/userguide/sp-applying.html
- 