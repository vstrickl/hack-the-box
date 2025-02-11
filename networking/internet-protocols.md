# The Internet Protocol

## Overview
**Internet protocols** are standardized rules and guidelines defined in RFCs that specify how devices on a network should communicate with each other.
-  Ensure that devices on a network can exchange information consistently and reliably, regardless of the hardware and software used.

## 2 Main Types of Connections on the Internet
- Transmission Control Protocol (TCP) -  a connection-oriented protocol that establishes a virtual connection between two devices before transmitting data
    - Transmits data by using a Three-Way-Handshake 
    - Slower than UDP because it requires additional overhead for establishing and maintaining the connection
    - **Example**: Websites
- User Datagram Protocol (UDP) - it does not establish a virtual connection before transmitting data
    - Considered a connectionless protocol
    - Sends the data packets to the destination without checking to see if they were received.
    - Less reliable than TCP because there is no guarantee that the packets will reach their destination.
    - **Example**: Youtube

## Internet Control Message Protocol (ICMP)
- Used to report errors or provide status information.
- Example: ping <target>
- A message in ICMP can be either a request or a reply
- Messages supported by ICMP include:
    - Error messages
    - Destination unreachable
    - Time exceeded messages

### Time-To-Live (TTL)
- A field in the ICMP packet header
- Limits the packet's lifetime as it travels through the network
- Prevents packets from circulating indefinitely on the network
- Can be used to determine the number of hops a packet has taken and the approximate distance to the destination
-  Tt is also possible to guess the operating system based on the default TTL value used by the device

***The user can change these values, so they should be independent of a definitive way to determine a device's operating system***

![ICMP](../images/Screenshot%202025-02-07%20at%203.05.07 PM.png)

## Voice over Internet Protocol (VoIP)
- A method of transmitting voice and multimedia communications
- Allows us to make phone calls using a broadband internet connection instead of a traditional phone line
- Most common VoIP ports are TCP/5060 and TCP/5061

### Session Initiation Protocol (SIP)
- A signaling protocol for initiating, maintaining, modifying, and terminating real-time sessions involving video, voice, messaging, and other communications applications and services between two or more endpoints on the Internet
- Uses requests and methods between the endpoints
- allows us to enumerate existing users for potential attacks such as:
    - Gain information about a user's availability, capabilities or services
    - Performing brute-force attacks on user accounts

#### Common SIP Request Methods
| Method   | Description |
|----------|------------|
| INVITE   | Initiates a session or invites another endpoint to participate. |
| ACK      | Confirms the receipt of an INVITE request. |
| BYE      | Terminates a session. |
| CANCEL   | Cancels a pending INVITE request. |
| REGISTER | Registers a SIP user agent (UA) with a SIP server. |
| OPTIONS  | Requests information about the capabilities of a SIP server or user agent, such as the types of media it supports, the codecs it can decode, and other details. |

##### The SIP `OPTIONS` request
- Allows us to enumerate users
- can probe a SIP server or user agent for information or test its connectivity and availability.