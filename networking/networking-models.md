# Networking Models

- 2 Networking Models 
    - [ISO/OSI model](../networking/osi-model.md)
    - TCP/IP model (Transmission Control Protocol/Internet Protocol) - many protocols that are responsible for the switching and transport of data packets on the Internet.
        - A generic term for the protocol family that provides the necessary functions for transporting and switching data packets in a private or public network
        - Allows hosts to connect to the Internet
            - The Internet is entirely based on the TCP/IP protocol family
        - Pen testers can quickly understand how the entire connection is established

    ![Model Layers](../images/Screenshot%202025-01-23%20at%201.35.29 PM.png)
    
- **Physical Layer / Network Layer** - Data is transmitted to the receiver

    ![PDU Pack Transfer](../images/Screenshot%202025-01-23%20at%201.40.35 PM.png)

*** *These networking models describe the communication and transfer of data from one host to another.*

## Vocabulary

- **encapsulation** - the process of each layer being added as a header to the PDU from the upper layer during the transmission of a packet
    - This controls and identifies the packet
    - The header and the data together form the PDU for the next layer

- **protocol data unit(PDU)** - the smallest unit of data that is transferred between devices in a network
    - Is transferred at a specific layer of a networking model