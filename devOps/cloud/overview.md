# Overview

## Resources as services

-  Resources such as physical assets, such as computers and hard disk drives, and virtual resources, such as virtual machines (VMs) are contained in data centers around the world.
  - These are split into regions, which are further split into zones
  - This distribution of resources provides several benefits, including
    -  redundancy in case of failure and
    - reduced latency by locating resources closer to clients.
  - Different resources can accessed globally, regionally or zonally
    - for example
      - global resources
        - preconfigured disk images, disk snapshots, and networks
        - creating a network is a global operation because a network is a global resource
      - Regional resources
        - static external IP addresses
        - reserving an IP address is a regional operation because the address is a regional resource.
      - zonal resources
        -  VM instances, their types, and disks
    - This prevents resources being misallocated and used inefficiently
      - you wouldn't want to attach a disk in one region to a computer in a different region because the latency you'd introduce would make for very poor performance.
- software and hardware products, become services.
  - These services provide access to the underlying resources.
  - When you develop your website or application on the cloud, you mix and match these services into combinations that provide the infrastructure you need, and then add your code to enable the scenarios you want to build.
- Projects (or similar name) are the combination of services used to run your application on the cloud
  - These are attached to your billing account, dashboard/console etc
