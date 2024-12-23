# Module 1 - Intro to AWS

- Client Server Model
  - Server is an app on EC2 (an instance)
  - client ie browser
  - Server ie app running on computer
    - a services like Amazon Elastic Compute Cloud (Amazon EC2)
  - client makes requests to server
    - The server evaluates requests, and fulfils it and sends response back to client
- Only pay for what you use (AWS key value)
  - For increased load -> increase EC2 instances to handle load
  - For decreased load -> decrease EC2 instances
  - Done manually or via rules which add/remove instances automatically
- Cloud computing
  - DEFN - The on demand delivery of IT resources over the internet with a PAYG pricing
    - on demand delivery -> AWS has the resources you need when needed, without telling them
    - IT resources -> like databases, memory etc
      - How you provision the resources does nto matter
      - What is on them (data), how it is structured, how its used does differentiate your buisness
      - Undifferentiated heavy lifting of IT - AWS helps with this part
  - Deployment models 
    - Cloud based
      - Run all parts of the application in the cloud.
      - Migrate existing applications to the cloud.
      - Design and build new applications in the cloud.
      - Can build on low level infrastructure that your IT staff maanges or use high level services that reduce management/architecting/scaling requirements
    - On Premises (private cloud deployment)
      - Deploy resources by using virtualization and resource management tools.
      - Increase resource utilization by using application management and virtualization technologies.
      - Resoources deployed on premises by using virtualization (docker) and resource management (K8s)
      - Similar to legacy IT, but tech used increases resource utilization
    - Hybrid
      - Connect cloud-based resources to on-premises infrastructure.
      - Integrate cloud-based resources with legacy IT applications.
      - Example: Connecting legacy app on site due regulations or better maintained, can pass off parts of the service to the cloud 
  - Benefits of Cloud
    - Trade upfrount expense for variable expense
      - Instead of buying resources upfront (ie data centers, physical servers) before using them -> upfront expense
      - Variable expense -> only pay for computing resources you consume
      - implement solutions while saving on costs
    - Stop spending money to run and maintain data centers
      - Allows you focus on the applications and customers
      - AWS handles this
    - Stop guessing capacity
      - Dont predict how much resources are needed
      - scale only in response to demand, rather than scaling earlier and over spending on extra unused resources
    - Massive economies of scale
      - reduce costs of buy resources on own
      - costs are cheaper, as more resources are bought in bulk at cheaper rates
    - Increase speed and agiilty
      - Easier to develop and deploy apps
      - Increase time to experiment and innovate 
      - Dont have to wait for time to procure
    - Go global in minutes
      - Due to reach of AWS, app is deployed globally to customers with low latency
- Links 
  - https://aws.amazon.com/getting-started/cloud-essentials/
  - https://d0.awsstatic.com/whitepapers/aws-overview.pdf
  - 