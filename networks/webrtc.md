# WebRTC (Web Real-Time Communication)

- [WebRTC (Web Real-Time Communication)](#webrtc--web-real-time-communication-)
    * [What](#what)
    * [Where used](#where-used)
    * [How](#how)
    * [Advantages](#advantages)
    * [When not to use](#when-not-to-use)
    * [Alternatives](#alternatives)
    * [Links](#links)


## What 

- a free and open-source technology and set of APIs that enable real-time communication and peer-to-peer data exchange directly between web browsers or other applications. 
- allows for audio, video, and data streaming without the need for plugins or external software

## Where used 

- Video Conferencing: 
  - enables browser-based video conferencing solutions, allowing users to participate in multi-party video conferences directly in their web browsers without requiring additional plugins or software.
- Voice and Video Calling: 
  - enables browser-to-browser voice and video calling, similar to traditional VoIP (Voice over Internet Protocol) applications. 
  - Users can initiate and receive calls directly from their web browsers.
- Live Streaming
  - real-time audio and video streaming, allowing content providers to deliver live video or audio feeds to their audience without the need for plugins or external media players.
- Screen Sharing
  - supports screen sharing capabilities, allowing users to share their screens with other participants in a web conference or collaboration session.
- File Sharing
  - With the data channel feature of WebRTC, users can exchange files or other data directly between their web browsers without relying on a central server.

## How 

- Key components 
  - MediaStream: 
    - allows access to audio and video streams from the user's device, such as a webcam or microphone, through the MediaStream API.
- RTCPeerConnection
  - This API facilitates peer-to-peer communication by establishing a connection between two devices or peers. RTCPeerConnection handles the negotiation and management of the media streams, codecs, and network protocols required for real-time communication.
- RTCDataChannel
  - WebRTC includes a data channel API that enables the exchange of arbitrary data between peers. This can be used for sending text messages, file transfer, or any other application-level data.

## Advantages
- Easy Implementation: 
  - provides a set of APIs and protocols that are built directly into modern web browsers, eliminating the need for additional plugins or software installations. 
  - easy to develop and deploy real-time communication applications without requiring users to install any additional components.
- Browser Compatibility: 
  - supported by major web browsers, including Chrome, Firefox, Safari, and Edge. 
  - This broad browser compatibility ensures that your WebRTC-based application can reach a wide range of users without compatibility issues.
- Real-Time, Low-Latency Communication:
  - designed for real-time communication, enabling low-latency audio, video, and data streaming between peers. 
  - It leverages peer-to-peer connections, minimizing the delay and reducing the need for centralized servers for media routing.
- Secure Communication
  - incorporates built-in encryption to ensure secure communication between peers.
  - uses Secure Real-time Transport Protocol (SRTP) for encrypting media streams, and Transport Layer Security (TLS) for securing the signaling process.
  - This helps protect against eavesdropping and ensures the privacy of communication.
- Peer-to-Peer Connectivity
  - establishes direct peer-to-peer connections between browsers or applications, allowing for efficient data transfer without the need for intermediate servers. 
  - reduces latency and reliance on central infrastructure, resulting in faster and more efficient communication.
- NAT and Firewall Traversal:
  - WebRTC includes mechanisms for traversing Network Address Translation (NAT) and firewall configurations, which can often be challenging for peer-to-peer communication.
  - utilizes techniques like Interactive Connectivity Establishment (ICE) and Session Traversal Utilities for NAT (STUN) to establish connections across different network configurations, enabling successful communication even in complex network environments.
- Versatile Media Support
  - supports audio, video, and data streaming, making it suitable for a wide range of real-time communication applications. 
  - includes codecs for audio and video compression, enabling efficient transmission of media streams.
- Mobile Support
  - allows for the development of real-time communication applications that can be accessed and utilized on smartphones and tablets.

## When not to use

- Legacy Browser Support may not support it
- Centralized Media Processing
  - If your real-time communication application requires complex media processing or transcoding
  - WebRTC primarily relies on peer-to-peer connectivity and is not optimized for server-side media processing. 
- Firewall Limitations
  - some network configurations or strict firewalls may still pose challenges
- Scalability and Centralized Control
  - webrtc may not be ideal for scenarios that require centralized control, routing, or scalability. 
  - Will need to use an alternative if need to manage large-scale real-time communication sessions, have centralized control over media routing, or require advanced features like recording and broadcasting
- Non-Real-Time Communication
  - If your application primarily focuses on non-real-time communication, such as asynchronous messaging or data transfer, WebRTC may be an unnecessary overhead and complexity
- Mobile Data Consumption
  - Real-time audio and video streaming over mobile networks can consume significant amounts of data, which can be a concern for users with limited data plans. 
  - should consider implementing adaptive bitrate streaming and other optimization techniques to minimize data usage and provide a better user experience.
- Lack of Scalability
  - WebRTC's peer-to-peer nature may not be suitable for scenarios that require large-scale, multi-party communication or centralized control.
  - Managing a large number of concurrent connections can be challenging, and implementing features like media routing, recording, and broadcasting may require additional infrastructure and complexity.
- Limited Media Control
  - WebRTC provides a standardized set of codecs and features, but it may not offer the same level of fine-grained control over media encoding, transcoding, or other advanced media processing capabilities compared to custom-built solutions or other protocols.

  
## Alternatives 

- SIP (Session Initiation Protocol): 
  - signaling protocol used for initiating, modifying, and terminating real-time sessions involving voice, video, and messaging applications.
  - widely used in Voice over IP (VoIP) and Unified Communications (UC) systems. SIP can be combined with other protocols and codecs to establish real-time communication channels.
- RTMP (Real-Time Messaging Protocol)
  - a protocol developed by Adobe for real-time streaming of audio, video, and data between a client and a server.
  - used for live streaming applications. 
  - Adobe has deprecated Flash and RTMP support in modern web browsers, reducing its relevance for web-based applications.
- MQTT (Message Queuing Telemetry Transport)
  - a lightweight publish/subscribe messaging protocol commonly used in Internet of Things (IoT) applications.
  - While it is not specifically designed for real-time communication, it can be utilized for lightweight and efficient messaging between devices and applications.
- XMPP (Extensible Messaging and Presence Protocol)
  - an open communication protocol used for instant messaging, presence information, and contact list management. 
  - often associated with chat applications and supports real-time text messaging, file transfer, and group chat functionality.
- H.323
  - a protocol suite used for audio, video, and data communication over IP networks. 
  - been widely used in traditional video conferencing systems and is still used in some enterprise environments.

## Links 