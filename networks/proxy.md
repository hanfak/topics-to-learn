# Proxy

## What?

- a proxy is typically a server, and it is a server that acts as a middleman between a client and another server. It literally is a bit of code that sits between client and server.
- the term proxy refers to a "forward" proxy.
  - A forward proxy is one where the proxy acts on behalf of (substitute for) the client in the interaction between client and server.
  - the server won't know that the client's request and its response are traveling through a proxy,
  - Forward proxies are used by individuals, businesses, and organizations to connect to the millions of websites and web servers on the internet. These users know that they are connecting to a proxy server.
  - VPNs
-  a reverse proxy - where the proxy acts on behalf of a server.
  - a reverse proxy is designed substitute for the server.
  - the client won't know that the request and response are routed through a proxy.
  - Reverse proxies are mainly used by web servers as a tool to balance the load they receive and to enhance the user experience by caching static content.
  - improve the security of web servers as they act as an additional layer that hackers have to get through before being able to reach the actual servers.
  -  users won’t necessarily know that it is connecting to a reverse proxy server.
  - Websites that receive huge amounts of traffic mostly use reverse proxies
  - load balancers
- Often clients won't even know that the network request got routed through a proxy and the proxy passed it on to the intended server (and did the same thing with the server's response).
- the proxy acts as a go-between or an intermediary between two different computers, enabling them to communicate effectively with each other
- Definition outside of computing
  - something or someone who is authorized to represent another person or object. Based on this globally accepted definition, there are two prerequisites to being a proxy:
    - Authorized: This means that the proxy is not acting on his or her own volition, but is only doing what the other party has allowed or authorized him or her to do.
    - To represent: The proxy is not acting for their own desires or preferences, but they are there in behalf of the other party.


## How

- If there was a middleman server that received requests, then sent them to another service, then forwards the response it got from that other service back to the originator client, that would be a proxy server.
- So when a client sends a request to a server via the proxy, the proxy may sometimes mask the identity of the client - to the server, the IP address that comes through in the request may be the proxy and not the originating client.
  - Example
    - access sites or download things that otherwise are restricted (from the torrent network for example, or sites banned in your country), you may recognize this pattern - it's the principle on which VPNs are built.

## Why?

- our reverse proxy can be delegated a lot of tasks that you don't want your main server handling
  - it can be a gatekeeper,
  - a screener,
  - a load-balancer and
  - an all around assistant.
- Anonymity
  - proxies mask the client’s real IP address and in effect, they also hide the client’s identity.
  - This allows users to use the internet anonymously, making them relatively safe from data brokers, their ISP, and even hackers.
- Caching
  - Proxies cache web pages and files that have been previously requested by the client.
  - If the client requests for the same page or file again, the proxy server will return the cached version, making connections faster and the browsing experience a lot better for the client.
- Secruity
  - When used together with an encryption protocol, proxies provide utmost security and privacy.
  - Proxy servers alone will anonymize the connection, but it doesn’t necessarily encrypt the traffic.
    - In effect, network traffic is still visible although tracing such traffic back to the client will be difficult.
  - Encrypting network traffic, however, will render all traffic unreadable to anyone.
- Bypass Restrictions
  - Not every website and webpage on the internet can be accessed by everyone.
  - Websites, corporations, and governments have imposed certain restrictions so that people in some countries won’t be able to access certain content.
  -  This is why we sometimes encounter error messages that say, “This content is not available in your location.”
  - By using proxies, however, clients can spoof their location, making web servers believe that they are located in a country where access to the content is not restricted.

## Uses?

- Proxy helps in anonymity. The proxy will always use a public IP and this is what the server will see.
- Proxies can be set so that all programs within a local network will have no choice but to use it.
- Proxies help you in getting the files cache, making a page load faster.
- Proxies helps in compressing network traffic, allowing the users to save their bandwidth.
- Proxies can remove ads from websites.
- Proxies help in content-filtering to ensure that internet usage within the organization abide to the policies of the organization.
- Proxies help in removing the referrers and change the User Agent string into a useless string. By doing this, the webpage server can’t obtain important information about the user.
- Proxies help in blocking suspicious and malicious websites.
- Proxies help you in bypassing censorship and geo location restrictions.

## Types

- Anonymous proxy
  - They act on behalf of the end-user, making the destination web server believe that it was they who made the request when in reality, somebody else is on the other end.
  -  Anonymous proxies obviously obfuscate the end user’s identity, which has increasingly become a necessity in today’s zero net neutrality world.
  - Using an anonymous proxy will keep clients from being bombarded with targeted ads, and will also keep them safe from identity theft.
    - This is done by discarding cookies that are injected when people visit websites which are further used to track the user’s every move.
- Elite Proxy or high anonymity proxies
  - give utmost security and privacy for internet users as they don’t come off as proxies to web servers.
  - They constantly change the IP address they use when communicating to web servers, so they can’t be detected as proxies.
  - Other people also use proxy switchers
  - Proxy or IP address switching is a very important feature especially since there are web servers who have developed a way to detect and block proxies. Elite proxies provide users with the ultimate disguise since the web servers have no idea that they are communicating with a proxy.
- Transparent Proxy
  - do not hide the IP address of the end-user
  - only to filter the content being passed through the network, and not to anonymize the user.
  - People who have used their company’s internet network may have come in contact with transparent proxies since offices, schools, and libraries usually use this type of proxies to be able to control what content the end-users can access within their network.
  - Transparent proxies provide no anonymity for the user at all.
- Distorting Proxy
  - works the same way as an anonymous proxy, although they have an additional feature that spoofs the user’s real location.
  - A distorting proxy sends a false IP address to the destination web server, making it believe that the request is from a certain location.
  - They are usually used as tools to get around geographical restrictions.
  - The feature that is common to all types of proxy is that they act on behalf of the user in requesting files or web pages from an external web server.
  - As the middleman, proxies can filter content that comes into the network and protect the identity of the user so the destination web server will never know sent the request.
- Private/paid Proxy
  - Private proxies give you a dedicated IP address that you can use exclusively. This means that the bandwidth and speed of connection are all yours to enjoy.
- Public/free proxy
  - are accessible to everyone.
  - Since hundreds or even thousands of people can be using the same server at a given time, using free proxies can slow down your connection speed.
  - hey are also unsafe as people with questionable intentions may also be using the same proxy server as you. You can end up getting banned even when you are not doing anything wrong.


## Links

- https://www.youtube.com/watch?v=ozhe__GdWC8&feature=emb_logo
