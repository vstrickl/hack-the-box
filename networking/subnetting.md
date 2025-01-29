# Subnetting

## Overview
- The division of an address range of IPv4 addresses into several smaller address ranges
- **subnet** - a logical segment of a network that uses IP addresses with the same network address
    - **subnet mask** - determines with the seperation occurs
- We can use subnetting to find out the outline of the respective network such as:
    - Network address
    - Broadcast address
    - First host
    - Last host
    - Number of hosts

## Using Subnetting to find the outline of a Network
💡 Remember IP address is divided into the network part and the host part
- The 1-bits in the subnet mask are fixed and cannot be changed
    - They determine the "main network" in which the subnet is located

![Network_Part](../images/Screenshot%202025-01-28%20at%2011.57.44 AM.png)

- The bits in the host part CAN be changed to the first and the last address
- The first address = the network address
    - Vital for the delivery of a data packet
    - If the network addresses are different, the data packet must be routed to another subnet via the default gateway
- The last address = the broadcast address

![subnetting](../images/Screenshot%202025-01-28%20at%2012.07.35 PM.png)

## Split the Network into x amount of Subnets
1. Start with the network address given

2. Identify what octet changes
- If the bits change to 0 in the host part that gives us the Network address

![network_address](../images/Screenshot%202025-01-28%20at%2012.09.38 PM.png)

- If the bits change to 1 in the host part that give us the Broadcast Address

![broadcast_address](../images/Screenshot%202025-01-28%20at%2012.11.21 PM.png)

*** ***We can only divide the subnets based on the binary system***

![binary_divide](../images/Screenshot%202025-01-28%20at%2012.13.26 PM.png)

3. Find out how big each subnet will be
- Find out the number of bits for the subnet mask by which we have to extend it
- Divide the network by by how much we have to extend it (ie. **Modulo Operation (%)**) and look at the remainder 
    - In this example our number is 4

![creating_subnets](../images/Screenshot%202025-01-28%20at%2012.15.42 PM.png)

- The leftover is the network bit reserved for the network mask

![creating_subnets](../images/Screenshot%202025-01-28%20at%2012.29.24 PM.png)

## Reminders
- 0 is a number in networking and does not = null
- The first address is the network
- The last is the broadcast address
- A subnet mask is 32-bits
    - The first part = the network part
    - the last = the host part
    - the number of bits per part is determined by the CIDR and what's left of the 32 bits