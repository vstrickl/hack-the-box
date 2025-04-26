# Initial Enumeration Steps

## Overview
To **enumerate** something means to systematically probe and gather detailed
information about your target for the purposes of identifying your potential entry piont for exploitation by gathering information on:
- [ ] Potential Vulnerabilities
- [ ] Misconfigurations
- [ ]

Information gathered from a target can be but is not limited to its:
- [ ] systems
- [ ] networks
- [ ] Services
- [ ] applications.

## Steps

#### 1. [Plan Your Attack](2_initial-steps.md)

#### 2. Ping the Target
Ping the target to make sure:
- [ ] It's reachable
- [ ] You're not getting a false positive

#### 3. Discover what ports are open
    - Scan all TCP ports to see what ports are open
    ```bash
    $ nmap -p- <target_ip>
    ```
    or
    ```bash
    $ nmap -sC -sV <target_ip>
