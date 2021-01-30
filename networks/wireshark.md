# Wireshark

- An application that helps analyse packets over tcp/ip.
- It is reverse proxy
- Help in diagnosing calls over the network
  - ie A curl request may not be sending the correct request, but the command looks correct. Wireshark will help see what was actually sent over the network

## Examples

- https://www.youtube.com/playlist?list=PLQnljOFTspQWSY37fn_xcOS0k1KjX_zsK

## Tips

- Always add deltat time column, set type to 'delta time displayed'

## Filters

- https://wiki.wireshark.org/DisplayFilters
- If syntax is correct turns green


### Examples

- ip.addr == 10.0.0.1
  - any packets to or from an ip address
  - More specific source ip `ip.src == 10.0.0.1` or destination `ip.dst == 10.0.0.1`
- `tcp` , `dns`
  - filters out the protocol used
  - Too much on many protocols `tcp or dns`
- tcp.port == 443
  - Find all packets using a tcp or udp port
  - for udp `udp.port == 444`
- tcp.analysis.flags
  - show any tcp problems ie packet loss
- !(arp or icmp or dns)
  - reduce noise of anything not useful
- click `follow tcp stream` from right click on packet
  - this will fill the filter, with `tcp.stream eq 32`
- tcp contains facebook
  - will search for any word in the packet
  - 'udp contains facebook' will look into udp packets (ie dns)
- http.response.code == 200
- http.request
- tcp.flags.syn == 1
  - look for syn attacks
- tcp.flags.reset == 1

## Links

- https://en.wikipedia.org/wiki/Wireshark
- https://www.wireshark.org/
- tutorial https://www.youtube.com/playlist?list=PLW8bTPfXNGdA_TprronpuNh7Ei8imYppX
