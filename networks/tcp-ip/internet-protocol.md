# IP - Internet Protocol

- The basic protocol that instructs us on how almost all communication across internet networks must be implemented.
- Messages over IP are often communicated in "packets",
  - which are small bundles of information (2^16 bytes).
  - Each packet has an essential structure made up of two components: the Header and the Data.
- Header
  - Contains "meta" data about the packet and its data.
  - his metadata includes information such as
    - the IP address of the source (where the packet comes from)
    - the destination IP address (destination of the packet).
- an IP Address
  - layer 3 property
  - Has Network and Host portion
  - is a numeric label assigned to each device connected to a computer network that uses the Internet Protocol for communication
  - There are public and private IP addresses,
  - there are currently two versions.
    - IPv6 and is increasingly being adopted because IPv4 (4 bytes = 32 bits) is running out out numerical addresses.
- other protocols are built on top of IP,
  - like frameworks built on languages
- Network vs Host
  - a.b.c.d/x
    - a,b,c,d are integers
    - x = defines the network, and the rest as host
  - Example: 192.168.254.0/24
    - the first 24 bits (3 bytes) are network
      - Max number of networks  2^24 and 2^8 hosts
    - the rest 8 bits are for host
    - subnet
      - subnet has a mask ie 255.255.255.0
      - used to determin if IP is in same subnet
- Default Gateway
  - Most networks consist of hosts and a default gateway
  - when host A want to talk to B directly if both are inthe same subnet, thus use mac address
    - OW A sends it to someone who might know the gateway
  - Has an IP add and each host should konw it's gateway



- https://youtu.be/o5S0-_vniiM The Beauty of the Internet Protocol hassan nasser
