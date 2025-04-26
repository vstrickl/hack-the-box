# 🔐 Port 443 Enumeration & Exploitation - AppSec Testing

## 📋 Port 443 Attributes

| Attribute            | Details                                               |
|----------------------|--------------------------------------------------------|
| **Port Number**      | 443                                                    |
| **Protocol**         | HTTPS                                                  |
| **Service**          | SSL/TLS                                                 |
| **Purpose**          | Secure communication over the web (encrypted HTTP)     |
| **Common Tools**     | Nmap, OpenSSL, ffuf, Gobuster, Burp Suite, Nikto, curl  |

**Context:** 
> *Testing extranet-accessible endpoint on port 443 to assess potential security risks of exposing an internal private cloud application.*
---

## 🌐 1. [Initial Enumeration](../../starting_point/2_initial-steps.md)

## 🧐 2. Confirm if port 443 is open

### 🔍 Basic Service Discovery
```bash
nmap -sS -Pn -p 443 <target> -oN nmap_443.txt
```
- Confirms if port 443 is open and responding to TCP connections.
- If not responding, check for the following restrictions:
- [ ] CDN
- [ ] [WAF](../restrictions/waf.md)
- [ ] Geo/IPh


---

### 🧪 Service & Version Detection
```bash
nmap -sV -p 443 --script ssl-enum-ciphers <target> -oN nmap_ssl.txt
```
- Detects SSL/TLS version, cipher suites, and certificate info.
- Flags deprecated protocols (e.g., SSLv2, TLS 1.0) and weak ciphers.

---

### 📜 Certificate Inspection
```bash
openssl s_client -connect <target>:443
```
- Review:
  - **Subject Alternative Names (SANs)** → Hints at internal hosts
  - **Common Name (CN)** → Validate consistency
  - **Validity Dates** → Look for expired certs
  - **Self-signed Cert?** → Poor trust validation
  - **Misconfigured Chain?** → Potential MitM angle

---

## 🧭 3. Web Application Discovery

### 📂 Directory & File Bruteforce
```bash
ffuf -u https://<target>FUZZ -w /usr/share/wordlists/dirb/common.txt -t 50 -mc all -o fuzz_443.json
```
- Discover exposed paths, login panels, config files, backups (`.bak`, `.zip`, `.old`)
- Test extensions: `.php`, `.asp`, `.jsp`, `.json`

---

### 🤖 Crawl with Tools
```bash
gobuster dir -u https://<target> -w common.txt -k -o gobuster_output.txt
```

---

## 🔒 4. Authentication & Session Security

### 🔐 Login Portal Analysis (if found)
- Check for:
  - **Lack of rate limiting** → Bruteforce user/password
  - **Exposed error messages** → Username enumeration
  - **Insecure cookies** → No `Secure`, `HttpOnly`, or `SameSite`
  - **Default credentials** → Try `admin/admin`, etc.

---

### 🔁 Token Analysis
- Use **Burp Suite** to inspect:
  - JWTs (check for `none` algorithm)
  - Reusable session tokens
  - Tokens in URL (not headers)

---

## 🛠️ 5. Exploitation Attempts

### 📬 HTTP Verb Tampering
```bash
curl -X HEAD https://<target>/admin
curl -X PUT https://<target>/api/test
```
- Test for logic flaws in how HTTP verbs are handled.

---

### 🧬 Exploitable Endpoints
- Look for:
  - **GraphQL**, **Swagger**, **actuator** endpoints
  - Hidden APIs (`/api/v1/debug`, `/internal/status`)
  - Parameter tampering or path fuzzing

---

### 🧼 Input Validation
- Use **Burp Intruder** or **ffuf** to inject:
  - SQLi payloads: `' OR 1=1--`
  - XSS: `<script>alert(1)</script>`
  - SSRF: `http://localhost:80`
  - LFI: `../../../../etc/passwd`

---

## 📉 6. Post-Exploitation & Lateral Movement (if applicable)

- Check for debug output or stack traces
- Try to pivot via SSRF or leaked internal DNS names
- Check for open admin portals (e.g., Jenkins, Jupyter, phpMyAdmin)
- Attempt to reuse session tokens for privilege escalation

---

## ✅ Recommendations

- Enforce WAF and rate-limiting
- Remove or hide debug endpoints
- Secure cookies and tokens
- Enforce strong cipher suites
- Use cert pinning if mobile clients are involved
