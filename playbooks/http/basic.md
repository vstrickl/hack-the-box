# 📌 Port 80 Enumeration and Exploitation (HTTP)

## Overview

| Attribute        | Details                                                               |
| ---------------- | --------------------------------------------------------------------- |
| **Port Number**  | 80                                                                    |
| **Protocol**     | HTTP                                                                  |
| **Service**      | Hypertext Transfer Protocol                                           |
| **Purpose**      | Web server communication                                              |
| **Common Tools** | nmap, nikto, gobuster, ffuf, dirb, whatweb, wafw00f, curl, Burp Suite |

---

## 🛠️ Enumeration Steps

### 1. Nmap Service Version and Script Scanning
```bash
nmap -sV -sC -p 80 <target-ip>
```
- Check for open services
- Identify web server type/version (Apache, Nginx, IIS, etc.)

---

### 2. Banner Grabbing
```bash
curl -I http://<target-ip>
```
- Gather HTTP headers
- Look for `Server`, `X-Powered-By`, or interesting info

---

### 3. Website Browsing
- Visit `http://<target-ip>` in a browser
- Look for login pages, default pages, directory listings
- Identify if it redirects (potential 443/HTTPS)

---

### 🔎 4. Check the website's SSL/TLS certificate

The certificate often lists the **common name (CN)** or **Subject Alternative Names (SANs)** = good clues.

```bash
openssl s_client -connect target-ip-or-domain:<port> -showcerts
```

- Look inside the certificate for `Subject` and `X509v3 Subject Alternative Name`.
- These often show real hostnames.

---

### 5. Technology Fingerprinting
```bash
whatweb http://<target-ip>
```
or
```bash
wafw00f http://<target-ip>
```
- Identify backend technologies (PHP, WordPress, ASP.NET, etc.)
- Detect Web Application Firewalls (WAFs)

---

### 6. Directory and File Bruteforcing

Find hidden directories, admin panels, configuration files

```bash
gobuster dir -u http://<target-ip> -w /usr/share/wordlists/dirb/common.txt
```
or
```bash
ffuf -u http://<target-ip>/FUZZ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

---

### 7. Vulnerability Scanning
```bash
nikto -h http://<target-ip>
```
- Check for known vulnerabilities (outdated software, misconfigurations)

---

## 🚨 Exploitation Steps

### 1. Default Credentials and Admin Pages
- Check common admin pages: `/admin`, `/login`, `/phpmyadmin`
- Attempt default credentials (admin:admin, admin:password, etc.)

---

### 2. File Upload Vulnerabilities
- Look for upload forms
- Attempt to upload web shells (e.g., PHP reverse shells)
- Bypass file type restrictions if necessary

---

### 3. Local File Inclusion (LFI)
- Test URL parameters for file inclusion:
  ```bash
  http://<target-ip>/index.php?page=../../../../etc/passwd
  ```

---

### 4. Remote Code Execution (RCE)
- If file uploads or vulnerable plugins are found, attempt RCE
- Examples:
  - Exploit vulnerable CMS plugins
  - Poison log files via User-Agent header (then include via LFI)

---

### 5. Command Injection
- Test input fields, URL parameters, and headers for injection:
  ```bash
  ;id
  && whoami
  | netstat -an
  ```

---

### 6. Cross-Site Scripting (XSS)
- Test for reflected or stored XSS:
  ```html
  <script>alert('XSS')</script>
  ```
- Check for cookie theft or session hijacking potential

---

### 7. SQL Injection
- Identify input fields connected to a database
- Use payloads like:
  ```sql
  ' OR '1'='1
  ```

---

## 🧹 Post-Exploitation
- Maintain access (upload web shells, create users, implant backdoors)
- Extract sensitive data (databases, config files)
- Look for pivoting opportunities (internal IPs, other services)

---

# ✅ Notes
- Always validate your findings (false positives are common).
- If a WAF is detected, be stealthy with your enumeration.
- Respect the testing scope and rules of engagement.