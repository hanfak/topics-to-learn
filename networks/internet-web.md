# Internet & Web

- a global network of billions of electronic devices. It is made up of a vast amount of independently operated networks. There is no central operating hub. All users are incentivized to make sure there is end to end activity which keeps things operating efficiently. The result is a mass of cables, computers, data centers, routers, servers, repeaters, satellites and wifi towers that allows digital information to travel around the world.

- https://monami555.github.io/2017/03/04/how-internet-works.html
- https://gist.github.com/alyssaq/6388253
- https://github.com/enkidevs/curriculum/wiki/Comp.-Sci.-networking-Course
- https://blog.codeanalogies.com/2018/04/26/web-servers-explained-by-running-a-microbrewery/

## Example Process

1. A client is a user-facing device (laptop, phone, etc.) that allows for internet transmitted data to be displayed.
2. The browser (Safari, Google Chrome, Firefox) is a platform within your client that displays the server-side information gathered by the internet.
3. This is done via the URI which is the web address (https://melanieharris.dev).
4. The Browser uses a domain name, which is located within the URI or an IP address (raw form of the domain name) to send a request for information. Remember, the IP address is similar to a mailing address. In order to deliver a package to someone, you must have specific location information.
5. DNS stands for Domain Name Server, it comes into play right after making a request to a domain name, your request goes to the DNS, an intermediary, who lookups and translates your domain name into its IP address.
6. The web browser, via the URI information, then connects to the webserver and sends an HTTP or HTTPS (secure) request. Via HTTP or HTTPS the requested information is either found or not found.
7. Once the data has been located and transmitted back, it will hit your firewall. The firewall will monitor incoming and outgoing network traffic and permit or blocks data packets (broken down pieces of data that will be resembled at the final destination) based on a set of security rules in order to block malicious traffic like viruses and hackers.
8. Next stop, the router. Your router will identify precisely where the data should go via the unique IP address. In other words, it identifies which client requested the date. Think of your router as your mailman or mailwoman. It’s their job to make sure packages are delivered to the correct name and address.
9. Once the correct client’s browser receives the request the connection is closed. The browser will parse through the data looking for elements needed to complete the page, this could be in form of audio, images, etc.. This step requires additional request until the page is completely loaded.

## Clients and Servers

- Client
  - hardware or software that accesses data made available by a storage system called a server. Clients include laptops, phones, and smart electronics to name a few. These devices are not directly connected to the internet like servers are. They connect directly to your internet service provider.
- Server:
  - also referred to as the back-end, is a computer (sometimes warehoused in large data centers) that stores data (webpages, sites, or apps) to be accessed by a client upon request.

## ISP - internet service provider

- an organization that provides services for communicating with the Internet, typically from a computer. Examples include Sky, BT.

## Web Browser

- a software application within your client for accessing information on the World Wide Web.
- Google Chrome, Safari, Firefox
- When a user requests a particular website, the web browser retrieves the necessary content from a web server and then displays the resulting web page on the user's device.
- It can render html and css into formatted pages
- Can run javascript
- Can handle certificates

## URI and URL
- Uniform Resource Identifier
  - URIs are the mechanism used by browsers to retrieve any published resource on the web.
  - In theory, each valid URI points to a unique resource. Such resources can be an HTML page, a CSS document, an image, etc.
- Uniform Resource Locator
  - A URL is a type of URI.
  - URI can be a name (URN), locator (URL), or both for an online resource, whereas a URL, is just the locator.
  - Examples of URLs include https://protocol or mailto:protocol. Example of URI https://example/path/to/author-image.png, where //example/path/to/image.jpg. is the name (URN).

## HTTP

- Hypertext Transfer Protocol  defines a language for clients and servers to speak to each other.
- This protocol defines how messages are formatted and transmitted, and what actions web servers and browsers should take in response to various commands.
- https://completedeveloperpodcast.com/episode-219/


## HTTPS

- This is a secure form of http
- The secure protocol adds an encryption layer for safety. Any site that handles sensitive information will use HTTPS.
- this Uses certificates

### Links

- https://gurunguns.wordpress.com/2017/10/10/how-does-https-works/
- https://robertheaton.com/2014/03/27/how-does-https-actually-work/
- https://gist.github.com/alyssaq/6377540
- https://stackoverflow.com/questions/6340918/trust-store-vs-key-store-creating-with-keytool
- https://www.youtube.com/watch?v=iQsKdtjwtYI
- https://javarevisited.blogspot.com/2012/09/difference-between-truststore-vs-keyStore-Java-SSL.html
- https://stackoverflow.com/questions/50401105/how-to-implement-tls-between-microservices
- https://security.stackexchange.com/questions/124714/how-to-make-secure-communication-between-servers

## TCP/IP

- Internet Protocol Address (IP Address):
  -  A unique identifier for everything directly or indirectly connected to the internet (clients, servers, etc.). Think of this in terms of a home address that uniquely defines the location of you or a neighbor.

### Links

- https://www.hostingadvice.com/blog/tcpip-make-internet-work/

## Domain Name

- easy to read addresses used for feasibility purposes. We typically use domain names instead of directly using numerical IP addresses. This practice was adopted because it is easier for humans to remember words rather than a string of numbers.
-  Examples include, MelanieHarris.dev or Google.com.

## DNS

- The intermediary that takes in the domain name, looks it up and then provides the corresponding IP address. Think of this as a phonebook, or a better example for the millennials reading this article, a decipher. It deciphers the domain name and provides the actual IP address for where the data is stored.

- https://scotch.io/tutorials/dns-explained-how-your-browser-finds-websites
- https://dyn.com/blog/how-does-dns-work/
- https://dyn.com/blog/dns-why-its-important-how-it-works/

### etc/hosts file

## OSI

- http://www.javaperspective.com/the-osi-model.html
- https://stackoverflow.com/questions/42456116/understanding-tcp-ip-layering-through-internet-flow
- http://www.javaperspective.com/ip-addresses-dns-and-port-numbers.html
- https://medium.com/@james_aka_yale/the-4-layer-internet-model-network-engineers-need-to-know-e78432614a4f

## Firewall

- a software program that prevents unauthorized access to or from a private network. Firewalls are tools that can be used to enhance the security of computers connected to a network, such as Local Area Network (LAN: a computer network that interconnects computers within a limited area) or the Internet.

## Router

- The mail carrier, so to speak. It is a networking device that forwards data (web page pieces called packets) between computer networks. It will make sure the correct information goes to the correct address. Routers perform the traffic directing functions on the Internet. If you are receiving your internet via fiber optic cables, the router is what transforms the light pulses into electrical signals which, via in ethernet cable, sends the signals to the client. If you are using cellular data, the pulses are sent to a cell tower then reaches a client such as a cell phone via electromagnetic waves.
