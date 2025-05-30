# Authenticaton Protocols

## Overview
- used in networking to verify the identity of devices and users
- provide a secure and standardized way of verifying the identity of:
    - users
    - devices
    - other entities in a network
- makie it difficult for attackers to gain unauthorized access and potentially compromise the network
- provide a means for securely exchanging information between entities in a network 
- ensures the confidentiality and integrity of sensitive data

## Common Authentication Protocols
| Protocol  | Description |
|-----------|-------------|
| Kerberos  | Key Distribution Center (KDC) based authentication protocol that uses tickets in domain environments. |
| SRP       | A password-based authentication protocol that uses cryptography to protect against eavesdropping and man-in-the-middle attacks. |
| SSL       | A cryptographic protocol used for secure communication over a computer network. |
| TLS       | A cryptographic protocol that provides communication security over the internet. It is the successor to SSL. |
| OAuth     | An open standard for authorization that allows users to grant third-party access to their web resources without sharing their passwords. |
| OpenID    | A decentralized authentication protocol that allows users to use a single identity to sign in to multiple websites. |
| SAML      | Security Assertion Markup Language is an XML-based standard for securely exchanging authentication and authorization data between parties. |
| 2FA       | An authentication method that uses a combination of two different factors to verify a user's identity. |
| FIDO      | The Fast IDentity Online Alliance is a consortium of companies working to develop open standards for strong authentication. |
| PKI       | A system for securely exchanging information based on the use of public and private keys for encryption and digital signatures. |
| SSO       | An authentication method that allows a user to use a single set of credentials to access multiple applications. |
| MFA       | An authentication method that uses multiple factors, such as something the user knows (a password), something the user has (a phone), or something the user is (biometric data), to verify their identity. |
| PAP       | A simple authentication protocol that sends a user's password in clear text over the network. |
| CHAP      | An authentication protocol that uses a three-way handshake to verify a user's identity. |
| EAP       | A framework for supporting multiple authentication methods, allowing for the use of various technologies to verify a user's identity. |
| SSH       | A network protocol for secure communication between a client and a server. It is used for remote command-line access, remote command execution, and secure file transfer. SSH uses encryption to protect against eavesdropping and other attacks and can also be used for authentication. |
| HTTPS     | A secure version of the HTTP protocol used for communication on the internet. HTTPS uses SSL/TLS to encrypt communication and provide authentication, ensuring that third parties cannot intercept and read the transmitted data. It is widely used for secure communication over the internet, particularly for web browsing. |
| LEAP      | A wireless authentication protocol developed by Cisco. It uses EAP to provide mutual authentication between a wireless client and a server and uses the RC4 encryption algorithm to encrypt communication. However, LEAP is vulnerable to dictionary attacks and other security vulnerabilities and has been largely replaced by more secure protocols such as EAP-TLS and PEAP. |
| PEAP      | A secure tunneling protocol used for wireless and wired networks. It is based on EAP and uses TLS to encrypt communication between a client and a server. PEAP uses a server-side certificate to authenticate the server and can also be used to authenticate the client using various methods, such as passwords, certificates, or biometric data. PEAP is widely used in enterprise networks for secure authentication. |

