# TCP/UDP Connections

## Overview
- Used in information and data transmission on the Internet

## Transmission Control Protocol (TCP)
- a connection-oriented protocol
- transmits data such as...
    - web pages
    - emails
- ensures that all data sent from one computer to another is received
- more reliable
- slower: more time is required for transmission and error recovery
- referred to as segments
- wrapped in the sent IP packet
- divided into headers and payloads
    - **payload**: contains the data that is being transmitted

### TCP Header Elements
- **source port**: indicates the computer from which the packet was sent.
- **destination port**: indicates where computer the packet is sent.
- **sequence number**: indicates the order in which the data was sent.
- **confirmation number**: used to confirm that all data was received successfully.
- **control flags**: indicate whether the packet:
    - marks the end of a message
    - is an acknowledgment that data has been received
    - contains a request to repeat data.
- **window size**: indicates how much data the receiver can receive.
- **checksum**: used to detect errors in the header and payload.
- **Urgent Pointer**: alerts the receiver that important data is in the payload.

### When an Error Occurs
- the receiver sends a message back so the sender can resend the missing data

## User Datagram Protocol (UDP)
- transfers datagrams between two hosts
    - **datagrams**: small data packets
- a connectionless protocol
    - does not need to establish a connection between the sender and the receiver before sending data.
    - data is sent directly to the target host without any prior connection
- transmit real-time data such as
    - streaming video
    - online gaming
    - Location like with Uber or Lyft
- used when speed is more important than reliability

### traceroute + UDP
- we will receive the following messages
    - Destination Unreachable
    - Port Unreachable
- generally UDP packets are sent using traceroute on Unix hosts

### Errors
- Does not verify if the received data is complete and error-free.
- The receiver does not receive this missing data if an error occurs
- no message will be sent back to resend the data

## Internet Protocol (IP) packet
- the data area used by the networking layer to transmit data from one computer to another
- consists of:
    - a header
        - the information on the sender and the recipient
        - instructions for where to send the data
    - the actual payload data

### IP ID
- Helpful to pay attention to because it helps identify a computer that has multiple IP addresses
- is used to identify fragments of an IP packet when fragmented into smaller parts
- is **16-bits**
- has a unique number ranging from **0-65535**
- the **IP ID** field will be different for each packet sent from the computer (but similar)
- **Network Sniffing**: can show you that two different IP addresses are sending packets to a particular IP address
    - **the IP ID** Should help you Identify the packets that are continuous
        - This strongly indicates that the two IP addresses belong to the same host in the network.

### IP Record-Route Field
- records the route to a destination device
- Contains a lists of IP addresses of all devices that passed through the **ICMP Echo Request** packet on the way to the destination device
- You get this through `ping` which shows the **Record-Route Field**
- **traceroute tool**: can be used to trace the route to a destination with accuracy
    - uses the TCP timeout method to determine when the route has been fully traced
    - The process repeats until:
        - the **TCP SYN packet** reaches the destination host and receives a **TCP SYN/ACK**
        - the **TCP SYN packet** gets a **TCP RST** response from the target
    ***Once we receive a response from the destination device, we know that we have traced the route to the destination and ended the traceroute process.***

#### Steps to determine when the route has been fully traced
| Step | Instructions |
|------|-------------|
| 1    | We send a TCP SYN packet to the destination device with a TTL of 1 in the IP header. |
| NOTE | When the TCP SYN packet with a TTL greater than 1 reaches a router, the value of the TTL is decreased by 1, and the packet is forwarded to the next device. If the TCP SYN packet with a TTL of 1 reaches a router, the packet is dropped, and the router sends an ICMP Time-Exceeded packet back to us. |
| 2    | We receive the ICMP Time-Exceeded packet and note the IP address of the router that sent the packet. |
| 3    | After that, we send another TCP SYN packet to the destination, increasing the TTL by 1. |

### IP Payload
- the actual payload of the packet
- contains the data from various protocols that are being transmitted

## Blind Spoofing
- a method of data manipulation in which an attacker sends false information on a network without seeing the actual responses sent back by the target devices.
- manipulates the IP header field to indicate false source and destination addresses
- It utilizes the **ISN** by sending a TCP packet to the target host with
    - a false **source port** number
    - false **destination port** numbers
    - a false ISN
        - **Initial Sequence Number (ISN)**: a field in the TCP header that is used to specify the sequence number of the first TCP packet in a connection
        - is set by the sender of a TCP packet
        - is sent to the receiver in the TCP header of the first packet
- Cause the target host to establish a connection with the attacker without receiving the connection
- used to:
    - disrupt the integrity of network connections
    - break connections between network devices
    - monitor network traffic
    - intercept information