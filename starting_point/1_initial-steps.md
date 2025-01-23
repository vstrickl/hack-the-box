# Initial Enumeration Steps

1) Make a plan and decide what you want to exploit

2) ping the target to make sure its reachable
- May get a false positive

3) Discover what ports are open
    - Scan all TCP ports to see what ports are open
    ```bash
    $ nmap -p- <target_ip>
    ```
    or
    ```bash
    $ nmap -sC -sV <target_ip>

4) Enumerate your target port(s) to determine vulnerabilities
    - Scan a specific port and get the service version info
    ```bash
    $ nmap -p <port> -sV <target_ip>
    ```

💡 Getting specific service version info allows operators to look up
known vulnerabilities and misconfigurations, determine attack
vectors, understand the target's environment, build a profile of the
target

**Note**
To enumerate Z means to systematically probe and gather detailed
information about a target for the purposes of identifying potential
vulnerabilities, misconfigurations, and entry pionts for exploitation
• Information gathered from a target can be but is not limited to its:
• systems
• networks
• Services
• applications.

## If You Don't Have an IP?
You can get target ips by enumerating the ASNs to get us a list of prefixes which then would give us a list of IPs
