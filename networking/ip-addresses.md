# IP Addresses

## Overview
- Ensures the delivery of data to the correct receiver
- **Media Access Control (MAC)** - what each host in the network located can be identified by.
    - Allows data exchange within the same network
    *** *If the remote host is located in another network, knowledge of the MAC address is not enough to establish a connection.*
- Addressing on the Internet is done via the IPv4 and/or IPv6 address
    - The IPv4 and IPv6 addresses are made up of the network address and the host address
    - IPv4 / IPv6 - describes the unique postal address and district of the receiver's building.
- It is possible for a single IP address to address multiple receivers (broadcasting) or for a device to respond to multiple IP addresses
- It must be ensured that each IP address is assigned only once within the network

## IPv4 Structure
- The most common method of assigning IP addresses
- Consists of a 32-bit binary number which is converted into more easily readable decimal numbers
- Each network interface is assigned a unique IP address.
- Allows for 4,294,967,296 unique addresses
- Divided into a host part and a network part
    - The router assigns the host part
    - The network administrator assigns the network part
- IANA allocates and manages the unique IPs on the internet

![IPv4_Addresses](../images/Screenshot%202025-01-28%20at%2011.10.51 AM.png)

## Classes
- The IP network blocks were divided into classes A - E

![Classes](../images/Screenshot%202025-01-28%20at%2011.15.05 AM.png)

## Subnetting
*[Link](./subnetting.md)*

- Dividing the classes into smaller networks
- **netmasks** - The proccess that creates the subnets
    - Is a long as the IPv4 address

![Subnetting](../images/Screenshot%202025-01-28%20at%2011.19.14 AM.png)

## Gateway Addresses
- **default gateway** - the name for the IPv4 address of the router that couples networks and systems with different protocols
    - It also manages addresses and the transmission methods
    - It is common for the ***default gateway*** to be assigned the first or last assignable IPv4 address in a subnet

![First_Address](../images/Screenshot%202025-01-28%20at%2011.22.41 AM.png)

## Broadcast Address
- Connects all devices in a network with each other
- **broadcast** - a message that is transmitted to all participants of a network and does not require any response
- a host can send a data packet to all other participants of the network simultaneously and still communicates its IP address
    - Receivers can use this IP address to contact it

![Last_Address](../images/Screenshot%202025-01-28%20at%2011.28.49 AM.png)

## The Binary System
- A number system that uses only two different states ON = 1 and OFF = 0
- The 32-bit binary number of an IPv4 address
    - Consists of into 4 bytes or octets
        - Which each equal an 8-bit group
            - These 8 bit groups range from 0-255

### How to calculate the value of an octet by its binary number

**Example IP** = *192.168.10.39*

![Calculate](../images/Screenshot%202025-01-28%20at%2011.43.43 AM.png)

![Octet_Value_192](../images/Screenshot%202025-01-28%20at%2011.35.38 AM.png)

![Result](../images/Screenshot%202025-01-28%20at%2011.44.48 AM.png)

## Classless Inter-Domain Routing (CIDR)
- A method of representing the subnet mask
    - It does this by specifying the number of 1-bits in the subnet mask
- Replaces the fixed assignment between IPv4 address and network classes
- The division is based on the subnet mask (ie. CIDR suffix)
    - **CIDR suffix** - indicates how many bits from the beginning of the IPv4 address belong to the network
- Allows the bitwise division of the IPv4 address space
- Allows you to get subnets of any size

![CIDR](../images/Screenshot%202025-01-28%20at%2011.51.51 AM.png)