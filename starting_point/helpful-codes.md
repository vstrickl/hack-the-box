# Helpful Codes

1) Scan and detect only the most common TCP ports
    - `$ nmap -sT <target_ip>`
    - `$ nmap -ps -pe <target_ip>`

## Notable flags:
- `-- min-rate`: speeds up the scan by specifying the number of packets that nmap should send per second. The higher the number, the faster the scan

**Notes**
When automating nmap be mindful of the following
- `for` loops can bog down the scan
- multi-threading can improve the speed of a scan
- be sure to always gather information when an item in a scan was:
    - 1st acquired
    - last updated
    - How is it configuration
    - What services is it running
    - What the proper configuration is
    - Is the target misconfigured
    - How can I utilize the misconfiguration