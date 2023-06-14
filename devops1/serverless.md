# Serverless 

- AWS lambdas
- work done when needed, rather than having an application sit idle doing nothing and waiting to do work

## Cons 

- Higher Costs:
  - While serverless can eliminate the need to pay for idle resources, the cost per CPU cycle on a serverless instance is often higher compared to traditional server-based instances. 
  - For long-running or resource-intensive tasks, serverless can be more expensive.
- Vendor Lock-In:
  - Serverless platforms are usually provided by cloud service providers, which can lead to vendor lock-in.
  - Once you build your application using specific serverless technologies and services, it can be challenging to migrate to another provider or architecture.
- Cold Start Delays:
  - Serverless functions have an inherent latency known as "cold start" delay. When a function is triggered after being idle for some time, there can be a delay in the function execution as the serverless platform provisions the necessary resources.
- Limited Execution Time:
  - Serverless functions often have execution time limitations imposed by the platform. 
  - If your function exceeds the time limit, it may be terminated, leading to potential issues for long-running processes.
- Complex Debugging and Monitoring:
  - Debugging and monitoring serverless applications can be more challenging compared to traditional architectures. Tracing requests and identifying issues in a distributed system of serverless functions can require specialized tools and approaches.
- Scalability Challenges:
  - While serverless platforms are designed to scale automatically, they may face limitations in terms of the maximum number of concurrent executions or processing capacity. High spikes in traffic or sudden bursts of workload can potentially exceed these limitations.
- Lack of Control and Customization: 
  - Serverless platforms abstract away much of the infrastructure management, which can be beneficial for simplicity. 
  - However, it also means that developers have less control over the underlying infrastructure and may face limitations in customization options.
- Dependency on Third-Party Services: 
  - Serverless often relies on various third-party services provided by the cloud provider, such as databases, storage, or authentication. 
  - If these services experience downtime or performance issues, they can impact the overall availability and performance of your serverless application.

## Patterns

- Basic event handling Processing events pushed to a queue by using a Lambda function.
- Scheduled jobs
  - Running scheduled tasks or processing files at specific intervals using serverless functions.
- Single-page application-centric design
  - Building the entire website experience on the front-end, coordinating systems and handling business logic.
- Aggregator services
  - Creating microservices that aggregate and format data from various services and databases for the single-page application.
- Throttling
  - Using serverless to handle traffic spikes by queuing requests and processing them at a rate that back office systems can handle.
- Image resizing
  - Uploading images to a bucket and using serverless functions to resize, process, and manipulate the images based on specific requirements.
- Orchestration
  - Using a controlling function to coordinate multiple serverless functions and manage their interactions.
- Reactive approach
  - Adding additional components, such as a ready check, to coordinate the completion of various services and trigger subsequent actions.
- Rapid development and scalability
  - Leveraging serverless frameworks and services for faster development and automatic scaling.
- Mitigation of errors
  - Serverless architecture helps mitigate errors by automatically refreshing instances and containers, reducing the impact of crashes or memory leaks.
- Denial of wallet attack
  - Considering the cost implications of excessive usage in highly trafficked services and deciding between traditional cloud instances and serverless options.
  
### links 

- https://serverlessland.com/patterns