# MAC Addresses

## Overview
- MAC addresses are 48-bits in total
    - With 6 octets (or bytes)
    - represented in hexadecimal format
    - The first half = the Organization Unique Identifier (OUI)
        - Defined by the Institute of Electrical and Electronics Engineers (IEEE) for respective manufactures
    - The last half = the Individual Address Part or Network Interface Controller (NIC)
        - Assigned by the manufacturer
            - Sets this bit sequence only once and ensures that the complete address is unique
- The physical address of our network interfaces
- The physical connection of a host
- Each network card has its individual MAC address
    - Configured once on the manufacturer's hardware side
    - Can always change (at least temporarily)
- must be addressed on layer 2 (the Routing layer) to the destination host's physical address or to the router / NAT when an IP packet is delivered
- Each packet has a sender address and a destination address
- If a host with the IP target address is located in the same subnet, the delivery is made directly to the target computer's physical address
- If the Ethernet frame's destination address matches its own layer 2 address, the router will forward the frame to the higher layers.
- **Address Resolution Protocol (ARP)** is used in IPv4 to determine the MAC addresses associated with the IP addresses.
- The local range is a reserved area for the MAC address

![Local_Range](../images/Screenshot%202025-01-28%20at%201.29.22 PM.png)

- Can be changed/manipulated or spoofed
    - DON'T rely on them as a sole means of security or identification
    - ALWAYS implement network segmentation and strong authentication protocols

## MAC Address Standards
- Ethernet (IEEE 802.3)
- Bluetooth (IEEE 802.15)
- WLAN (IEEE 802.11)

## MAC Address Decimal Representation

![subnetting](../images/Screenshot%202025-01-28%20at%201.10.17 PM.png)

## The last 2 bits in the first octed of a MAC address

### The last bit
- Only has binary states
- Identifies the MAC address as either:
    - 0 = Unicast
        - Packet will reach only 1 host
    - 1 = Multicast
        - Packet is sent 1x to all hosts on the local network
            - These networks will decided whether or not to accept to packet based on their configuration

![Unicast](../images/Screenshot%202025-01-28%20at%201.32.53 PM.png)

### The 2nd to the last bit
- Identifies whether it is a **global OUI** or a **locally administrated** MAC address
- The **global OUI** is defined by the IEEE

![2nd_2_last_bit](../images/Screenshot%202025-01-28%20at%201.41.15 PM.png)

## Broadcast
- When data packets are transmitted simultaneously from one point to all members of a network
- Used if the address of the receiver of the packet is not yet known

![broadcast](../images/Screenshot%202025-01-28%20at%201.36.14 PM.png)

## MAC Address Attack Vectors

- **MAC spoofing**: Altering the MAC address of a device to match that of another device.
    - Allows the attacker to gain unauthorized access to a network.

- **MAC flooding**: Sending many packets with different MAC addresses to a network switch.,
    - This causes the MAC address table to reach its capacity and prevent it from functioning correctly.

- **MAC address filtering**: Some networks may be configured only to allow access to devices with specific MAC addresses.
    - An attacker can exploit this by gaining access to the network using a spoofed MAC address.

## Address Resolution Protocol (ARP)
- An network protocol used to resolve the Network layer IP Address (Layer 3 of the OSI model) to a link layer MAC Address (Layer 2 - Routing Layer).
- Map's a host's IP address to its corresponding MAC address to facilitate communication between devided on a Local Area Network (LAN)
- **ARP resolution** the process of a device on a LAN communicating with another device by sending a broadcast message that contains: 
    - The destination IP address
    - Its own MAC address
    - The devide with the matching IP address responds with its own MAC address
- Allows devices to send and recieve data using MAC addresses rather than IP Addresses to allow for better efficiency

### 2 Types of ARP Request Messages
- **ARP Request** = the process of resolving the destination devices IP address to its MAC address.
    - Broadcast to all devices on the LAN
- **ARP Reply** - The process of a device recieving an ARP request.
    - When a device with the matching IP recieves the ARP request it responds with:
        - its MAC address

![arp_request](../images/Screenshot%202025-01-28%20at%201.59.04 PM.png)

## ARP Attack Vectors
- **ARP Spoofing** - The process of intercepting or manipulating traffic intended for the legitimate device on the network
    - *Other Names*: ARP cache poisoning or ARP poison routing
    - **Tools** - ***Ettercap*** or ***Cain & Abel***
        - send falsified ARP messages over a LAN
    - **Attacker Goal**: associate the target MAC address with the IP address of a legitimate device on the target's network.
        -  stealing sensitive information
        - Redirect Traffic
        - Launch MITM attacks
    - **Security Measure** - Implement firewalls and intrusion detection systems, use secure network protocols, (ie. IPSec or SSL)

[arp_spoofing](../images/Screenshot%202025-01-28%20at%202.06.29 PM.png)

- The first and fourth lines shows the attacker sending falsified ARP messages to the target
- The second and third lines show the target sending an ARP request and replying to the attacker's MAC address.