# Module 4 Networking

- Virtual private cloud (VPC)
  - aLLows to configure services into private (only internal) and public (accessed via internet) subnets

## Connectivity to AWS 

- VPC Amazon Virtual Private Cloud
  - Without it all your resources will be accessible
  - Helps establish boundaries
  - Define own private IP range for resources (ie EC2 and ELB)
  - Place resources (Defined by the IP ranges) into different subnets, allow groupings of IP ranges
    - Subnet is a section of VPC that can contain resources
  - Different subnets can have different configurable networking rules (to make public or private)
  - Public resources
    - want customers to access
    - Need to attach an Internet Gateway to the VPC, allows outside traffic in to VPC
  - PRivate resources
    - only those logged into VPC can access (databases, internal services )
    - Setup a Virtual Private Gateway to the VPC for the private networks
      - create a VPN connection between the VPC and the internal corporate network
    - Only authenticated users can access
    - Still use the internet, so shared bandwidth by other users -> slow downs
      - so VPG must be dedicated and not shared -> meet regulartory and compliance needs
      - Use AWS Direct Connect
        - creates physical line directly from one network to private network

### Links
 
## Subnets and Network Access Control Lists

- Network Hardening
  - Subnets control access
  - The Packets get checked against the Network ACL at the subnet boundary
    - Virtual Firewall controls traffic at the subnet level
    - Checks whether packet has access to leave or enter subnet 
    - Like a passport control 
    - Does not check if it can reach a specific resource or instances 
    - Stateless, always checks entering and leaving subnet
    - Each AWS account includes a default network ACL
      - It allwos all in and out traffic
      - Can modify by adding rules
    - For Custom network ACL
      - all inbound and outbound traffic is denied until you add rules to specify which traffic to allow
  - Instnace level security
    -  All instances, when launched come with a security group
    - By default no packets allowed in, all ports are blocked
    - Owner configures SG, to allow specific type of traffic in 
      - ie allow Https, but not OS or admin
      - This updates a list of who are authorised to enter
    - They dont check traffic coming out of SG, all traffic out
    - Is stateful
      - on the response coming back is rememberd by the security group and allows it in

### Limks 

- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html
- https://docs.aws.amazon.com/vpc/latest/userguide/vpc-security-groups.html

## Global Networking

- Route 53 
  - Domain Name service (DNS)
  - Translates website names (url/hostnames) to ip addresses
  - Then routes request to that address
  - Has several routing policies
    - latency based
    - geolocation dns
      - traffic from a specific area is routed to specific area (the ip address in that location)
    - geoproximity 
    - weighted round robin
  - Register domain names
  - Transfer dns records for existing domain names managed by other domain registrars.
- Cloudfront
  - CDN 
  - a network that helps to deliver edge content to users based on their geographic location. 
  - Store static assets closer to the users

## Links 

- https://aws.amazon.com/products/networking
- https://aws.amazon.com/blogs/networking-and-content-delivery/
- https://aws.amazon.com/vpc
- https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html
- https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html