# Key Exchange Mechanisms

## Overview
- The security of the encryption used to protect communication relies on the secrecy of the keys.
- Key Exchange Mechanisms are used to exchange cryptographic keys between two parties securely
- Common methods work by allowing the two parties to agree on a **shared secret key** over an insecure communication channel that encrypts the communication between them
    - done using some form of mathematical operation

## Mathmatical Operations for Key Exchange Methods

### Diffie-Hellman
- Allows two parties to agree on a shared secret key without any prior communication or shared private information
- Allows two parties to generate a shared secret key that can be used to encrypt and decrypt messages between them
- used as the basis for establishing secure communication channels (ie. **TLS**)

#### Limitations
- equires a relatively large amount of CPU power
    - impractical for...
        - use in low-power devices
        - situations where the key needs to be generated quickly
- vulnerable to MITM attacks
    - **MITM attack**: the attacker...
        - intercepts the communication between the two parties
        - pretend to be one of the parties
        - generates a different secret key
        - Tricks both parties into using the false key
        - allows the attacker to read and modify the messages sent between the parties

### Rivest–Shamir–Adleman (RSA)
- Uses the properties of large prime numbers to generate a shared secret key
- Relies on the fact that it is relatively easy to multiply large prime numbers together
- Makes it challenging to factor the resulting number back into its prime factors

#### Applications and protocols that use RSA
- Encrypting and signing messages to provide confidentiality and authentication
- Protecting data in transit over networks, such as in the Secure Socket Layer (SSL) and TLS protocols
- Generating and verifying digital signatures, which are used to provide authenticity and integrity for electronic documents and other digital data
- Authenticating users and devices, such as in the Public Key Cryptography for Initial Authentication in Kerberos (PKINIT) protocol used by the Kerberos network authentication system
- Protecting sensitive information, such as in the encryption of personal data and confidential documents

### Elliptic curve Diffie-Hellman (ECDH)
- a variant of Diffie-Hellman key exchange
- uses elliptic curve cryptography to generate the shared secret key
- more efficient and secure than the original Diffie-Hellman in ways such as 
    - Establishing secure communication channels, such as in the TLS protocol
    - Providing forward secrecy, which ensures that past communications cannot be revealed even if the private keys are compromised
    - Authenticating users and devices, such as in the Internet Key Exchange (IKE) protocol used in VPNs

### Elliptic Curve Digital Signature Algorithm (ECDSA)
- uses elliptic curve cryptography to generate digital signatures
- authenticates the parties involved in the key exchange

| Algorithm                                 | Acronym | Security |
|-------------------------------------------|---------|-------------------------------------------------------------|
| Diffie-Hellman                            | DH      | Relatively secure and computationally efficient             |
| Rivest–Shamir–Adleman                     | RSA     | Widely used and considered secure, but computationally intensive |
| Elliptic Curve Diffie-Hellman             | ECDH    | Provides enhanced security compared to traditional Diffie-Hellman |
| Elliptic Curve Digital Signature Algorithm | ECDSA   | (No security description provided)                           |

## Internet Key Exchange
- a protocol used to establish and maintain secure communication sessions (ie. VPNs)
- a key component of many VPN solutions
- enables the secure exchange of keys and other security information between the VPN client and server
- allows the VPN to establish an encrypted tunnel through which data can be transmitted securely.
- Uses a combination of the Diffie-Hellman key exchange algorithm and other cryptographic techniques to securely exchange keys and negotiate security parameters
- Also used for the authentication of users and devices
- Used in conjunction with other protocols and algorithms, such as...
    - **RSA**: key exchange and digital signatures
    - **Advanced Encryption Standard (AES)**: data encryption.

### 2 Operating Modes of IKE
- **main mode**: default mode
    - considered more secure
    - key exchange process is performed in three phases
        - each phase exchanges a different set of security parameters and keys
    - provides greater flexibility and security
    - slower in performance
- **aggressive mode**: reduces the number of round trips and message exchanges required for key exchange
    - the key exchange process is performed in two phases
    - faster performance
    - all security parameters and keys are exchanged in the first phase
    - less secure

### Pre-Shared Key (PSK)
- a secret value shared between the two parties involved in the key exchange
- used to authenticate the parties and establish a shared secret that encrypts subsequent communication
- must be securely exchanged between the two parties before the key exchange process begins
    - done through a secure out-of-band channel, such as...
        - separate communication channel
        - physically exchange
- provides an additional layer of security by allowing the parties to authenticate with each other
- optional

#### Limitations
- difficult to exchange the key securely
- the security of the IKE session may be compromised if the key is compromised through an MITM attack