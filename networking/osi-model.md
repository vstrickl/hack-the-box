# The OSI Model

## Definition
ISO/OSI model or Open Systems Interconnection (OSI) is a reference model that can be used to describe and define the communication between systems
- dictates strict rules and protocols that systems must follow for communication
- a communication gateway between the network and end-users
- referred to as the reference model
- known for its strict protocol and limitations
- Pen Testers can take the system apart piece by piece and analyze it in detail

![The OSI Model Layers](../images/Screenshot%202025-01-23%20at%201.23.44 PM.png)

### The 7 Individual layers of the OSI model
1. Physical
2. Data Link
3. [Network](./network-layer.md)
4. Transport
5. Session
6. Presentation
7. Application

![The OSI Model Layers Definitions](../images/Screenshot%202025-01-23%20at%201.51.51 PM.png)

- Each layer has clear seperate tasks
- Are hierarchically based on each other to achieve the OSI model goal
    - Each layer offers services for use to the layer directly above it
- Represent a phase in the establishment of each connection through which the sent packets pass
- layers 2-4 are transport oriented
- layers 5-7 are application oriented
- If two systems communicate, all seven layers of the OSI model are run through at least twice

## Goal
Create a reference model that enables the communication of different technical systems via various devices and technologies and provides compatibility