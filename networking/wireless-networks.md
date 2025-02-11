# Wireless Networks

## Overview
Wireless networks are computer networks that use wireless data connections between network nodes
- use radio frequency (RF) technology to transmit data between devices
- Each device on a wireless network has a wireless adapter that converts data into RF signals and sends them over the air.
- to connect to a wireless network, a device must be within range of the network and configured with the correct network settings
- Communication between devices occurs over RF in the 2.4 GHz or 5 GHz bands in a WiFi network
- The strength of the RF signal and the distance it can travel are influenced by:
    - The transmitter's power
    - The presence of obstacles
    - The density of RF noise in the environment.

***WiFi networks use techniques such as spread spectrum transmission and error correction to overcome these challenges to ensure reliable communication***

## Process
When a device, like a laptop, wants to send data over the network...
1. It communicates with the Wireless Access Point (WAP) to request permission to transmit
2. The WAP connects the wireless network to a wired network and controls access to the network.
3. Once the WAP grants permission, the transmitting device sends the data as RF signals
4. These signals are received by the wireless adapters of other devices on the network
5. The data is then converted back into a usable form and passed on to the appropriate application or system

## WAP Requests
- **Connection request frame (ie. association request)**: A request a device makes to the WAP to initiate the connection process
    - Uses **IEEE 802.11**: A wireless networking protocol that defines the technical details of how wireless devices communicate with each other and with WAPs

### Connection Request Details
| Parameter                     | Description |
|--------------------------------|------------|
| MAC address                   | A unique identifier for the device's wireless adapter. |
| SSID                          | The network name, also known as the Service Set Identifier of the WiFi network. |
| Supported data rates          | A list of the data rates the device can communicate. |
| Supported channels            | A list of the channels (frequencies) on which the device can communicate. |
| Supported security protocols  | A list of the security protocols that the device is capable of using, such as WPA2/WPA3. |

## WEP Challenge-Response Handshake
-  A process to establish a secure connection between a WAP and a client device in a wireless network that uses the WEP security protocol

| Step | Who   | Description |
|------|------|-------------|
| 1    | Client | Sends an association request packet to the WAP, requesting access. |
| 2    | WAP    | Responds with an association response packet to the client, which includes a challenge string. |
| 3    | Client | Calculates a response to the challenge string and a shared secret key and sends it back to the WAP. |
| 4    | WAP    | Calculates the expected response to the challenge with the same shared secret key and sends an authentication response packet to the client. |

### Errors with the WEP Handshake
- Cyclic Redundancy Check (CRC) is an error-detection mechanism used in the WEP protocol to protect against data corruption in wireless communications.
    - When the destination device receives the packet, the CRC value is recalculated and compared to the original value.
- design of the CRC mechanism has a flaw that allows us to decrypt a single packet without knowing the encryption key
    - CRC value is calculated using the plaintext data in the packet rather than the encrypted data

## WiFi Security Features
- Encryption - uses algorithms to protect the confidentiality of data transmitted over wireless networks. 
    - common encryption algorithms in WiFi networks are:
        - Wired Equivalent Privacy (WEP)
        - WiFi Protected Access 2 (WPA2)
        - WiFi Protected Access 3 (WPA3).
- Access Control
- Firewall - a security system that controls incoming and outgoing network traffic based on predetermined security rules

### WEP Encryption
- Uses a 40-bit or 104-bit key to encrypt data
- Not compatible with newer devices and operating systems
- Uses the RC4 cipher encryption algorithm (which is vulnerable to attacks)
- uses a shared key for authentication
- WEP Protocol:
    - **Version: WEP-40/WEP-64**: uses a 40-bit (secret) key
    - **Version: WEP-104**: uses a 104-bit key
    - Protocol parts:
        - **Initialization Vector (IV)**
            - used to create the key for both WEP-40 and WEP-104 
            - Small value
            - Ensurea that each key is unique
        - **secret key**: used to encrypt the data

| Protocol      | IV      | Secret Key |
|--------------|--------|------------|
| WEP-40/WEP-64 | 24-bit | 40-bit     |
| WEP-104      | 24-bit | 80-bit     |

### WPA Encryption
- When paired with the Advanced Encryption Standard (AES) it uses a 128-bit key
- Longer keys are still vulnerable to various attacks that can allow an attacker to decrypt data transmitted over the network
- Pre-Shared Key (PSK) or an 802.1X authentication server as an authentication method
- Compatible with most devices and operating systems
- Protocols WPA2 and WPA3
- 2 main versions are
    - WPA-Personal
    - WPA-Enterprise

## Authentication Protocols
- **Extensible Authentication Protocol (EAP)**: a framework for authentication used in various networking contexts
- **Lightweight Extensible Authentication Protocol (LEAP)**: uses a shared key for authentication
    - the same key is used for encryption and authentication
- **Protected Extensible Authentication Protocol (PEAP)**: uses tunneled TLS
    - the encrypted tunnel protects the authentication process
    - **Transport Layer Security (TLS)**: establishes a secure connection between the device and the WAP using a digital certificate

## Terminal Access Controller Access-Control System Plus (TACACS+) server
- encrypts the entire request packet to protect the confidentiality and integrity of the request
- used for routers and switches
- includes the user's credentials and other information about the session
- Encryption methods:
    - SSL/TLS
    - IPSec

## Disassociation Attack
- a type of all wireless network attack that aims to disrupt the communication between a WAP and its clients
- The attack sends disassociation frames to one or more clients
    - WAP uses disassociation frames to disconnect a client from the network
- can launch the attack from within or outside the network depending on our location and network security measures
- Can use it as a precursor to other attacks, such as a MITM attack

## Wireless Hardening
- The process of protecting the wireless networks
- Methods include:
    - **Disabling broadcasting of the SSID**: makes  it more difficult to discover and connect to the network
        - the WAP will not transmit beacon frames, 
    - **WiFi Protected Access (WAP)**: provides strong encryption and authentication for wireless communications
        - protects against unauthorized network access and sensitive data interception
    - **MAC filtering**: the process of allowing a WAP to accept or reject connections from specific devices based on their MAC addresses
        - prevents unauthorized devices from connecting to the network
    - **EAP-TLS**: a security protocol used to authenticate and encrypt wireless communications
         - uses digital certificates and PKI to verify the identity of clients and establish secure connections
         - Deploying with **EAP-TLS** can protect against unauthorized access to the network and the interception of sensitive dat

