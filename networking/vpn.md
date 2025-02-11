# Virtual Private Network (VPN)

## Overview
- a technology that allows a secure and encrypted connection between a private network and a remote device
- allows the remote machine to access the private network directly from any location
- provides secure and confidential access to the network's resources and services
- they encrypt the connection between the remote device and the private network
- uses the public internet to connect remote users to the private network
- **TCP/IP layer**: the connection uses the **Encapsulating Security Payload (ESP)** protocol to encrypt and authenticate the VPN traffic

### Typical VPN Ports
- **TCP/1723**:for Point-to-Point Tunneling Protocol PPTP VPN connections
- **UDP/500**: for IKEv1 and IKEv2 VPN connections

### Components and Requirements for the VPN
| Requirement    | Description |
|---------------|-------------|
| VPN Client    | This is installed on the remote device and is used to establish and maintain a VPN connection with the VPN server. For example, this could be an OpenVPN client. |
| VPN Server    | This is a computer or network device responsible for accepting VPN connections from VPN clients and routing traffic between the VPN clients and the private network. |
| Encryption    | VPN connections are encrypted using a variety of encryption algorithms and protocols, such as AES and IPsec, to secure the connection and protect the transmitted data. |
| Authentication | The VPN server and client must authenticate each other using a shared secret, certificate, or another authentication method to establish a secure connection. |

## Internet Protocol Security (IPsec)
-  network security protocol that provides encryption and authentication for internet communications
- encrypting the data payload of each IP packet and adding an AH

### 2 Protocols IPSec uses to provide encryption and authentication
- **Authentication Header (AH)**: used to verify the integrity and authenticity of the packet
    - Does not provide encryption.
    - Adds an authentication header to each IP packet
        - Eash header of the IP packet contains a cryptographic checksum that can be used to verify that the packet has not been tampered with.
- **Encapsulating Security Payload (ESP)**: a protocol that provides encryption and optional authentication for IP packets
    - It encrypts the data payload of each IP packet and optionally adds an authentication header, similar to AH.
***These protocols provide the security and encryption that are required for secure communication over the public internet***

### 2 Modes of IPSec
| Mode          | Description |
|--------------|-------------|
| Transport Mode | In this mode, IPsec encrypts and authenticates the data payload of each IP packet but does not encrypt the IP header. This is typically used to secure end-to-end communication between two hosts. |
| Tunnel Mode   | With this mode, IPsec encrypts and authenticates the entire IP packet, including the IP header. This is typically used to create a VPN tunnel between two networks. |

## Point-to-Point Tunneling Protocol (PPTP)
- a network protocol that enables the creation of VPNs by establishing a tunnel between the VPN client and server
- Encapsulates the data transmitted within the tunnel
- It can tunnel protocols such as:
    - IP
    - IPX
    - NetBEUI via IP
- PPTP has too many known vulnerabilites so it is no longer considered secure
    - Its authentication method, MSCHAPv2, employs the outdated DES encryption, which can be easily cracked with specialized hardware.
- It has been largely replaced by more secure VPN protocols like
    - L2TP/IPsec
    - IPsec/IKEv2
    - OpenVPN