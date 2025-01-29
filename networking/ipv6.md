# IPv6 Addresses

## Overview
- The sucessor of IPv4
    - Expected to completely replace IPv4
- 128-bits long
- The prefis identifies the host and network parts
- the **Internet Assigned Numbers Authority (IANA)** is responsible for assigning IPv4 and IPv6 addresses and their associated network portions
- Available simultaneously with IPv6 making it a **Dual Stack**
- Consistently follows the **end-to-end princilple** which emphasizes that specific functions (ie. error correction, encryption, and reliability) should be implemented at the endpoints of a communication system rather than in intermediary nodes (eg. routers or switches)
- Provides publicly accessible IP Addresses for any end devices without the need for NAT
- An interface can have multiple IPv6 addresses
- Consists of 2 parts
    - Network Prefix = the network part
        - Identifies the network, subnet or address range
    - Interface Identifier (aka suffix) = the host part
        - formed from the 48 bit MAC address or the interface
            - Converted to a 64-bit address
## Typica IPv6 Prefix Lengths
- Default = `/64`
- `/32`
- `/48`
- `/56`

***If we want to use our network we the a shorter prefix than `/64` from our provider***

## IPv6 Advantages over IPv4
- Larger address space
- Address self-configuration (SLAAC)
- Multiple IPv6 addresses per interface
- Faster routing
- End-to-end encryption (IPsec)
- Data packages up to 4 GByte

[IPv6_IPv4_Comparison](../images/Screenshot%202025-01-28%20at%202.20.03 PM.png)

## 4 Different Types of IPv6 Addresses
- **Unicast** - Addresses for a single interface.
- **Anycast** -	Addresses for multiple interfaces
    - Only one of them receives the packet.
- **Multicast** - Addresses for multiple interfaces
    - All receive the same packet.
- **Broadcast** - Does not exist
    - Realized with multicast addresses.

## The Hexadecimal System
- Use the make the binary representation more readable

[The_Hexadecimal_System](../images/Screenshot%202025-01-28%20at%202.24.28 PM.png)

- Converting 192.168.12.160 to IPv6

[Converting_to_Hex](../images/Screenshot%202025-01-28%20at%202.26.37 PM.png)

- Then divide the total 128 bits (total IPv6 bits) by the 8 (the total number of octets).
- The multiply that by 16 (4 hex numbers)
    - These 4 hex numbers are grouped and seperated by a colon (:)
- To simplify or shorten the address you can replace any 4 zeros with (::)

### Result
- **Full IPv6**: fe80:0000:0000:0000:dd80:b1a9:6687:2d3b/64
- **Short IPv6**: fe80::dd80:b1a9:6687:2d3b/64

## Request for Comments (RFC) 5952
- Deifnes the IPv6 address notation as:
    - All alphabetical characters are always written in lower case.
    - All leading zeros of a block are always omitted.
    - One or more consecutive blocks of 4 zeros (hex) are shortened by two colons (::).
    - The shortening to two colons (::) may only be performed once starting from the left.