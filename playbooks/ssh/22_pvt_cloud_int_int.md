# 📚 Port 22 (SSH) Overview

## Overview
| Attribute            | Details                     |
|----------------------|------------------------------|
| **Port Number**       | 22                           |
| **Protocol**          | TCP                          |
| **Service**           | SSH (Secure Shell)           |
| **Purpose**           | Remote login, file transfer, remote command execution |
| **Common Tools**      | `ssh`, `sftp`, `scp`, `rsync`, custom tunnels |

## Legitimate Use Cases for Testing SSH
The following a use cases for proposing a limited and secured security testing
- automated deployment between apps over SSH
- file transfers over SCP/SFTP
- agent connections using SSH

**Important:**  
- SSH is often used internally for administrative access, service communication, and automated deployments.
- Misconfigured or outdated SSH services can expose serious vulnerabilities (weak ciphers, default credentials, privilege escalation paths).

---

# 🛠️ Port 22 Enumeration Steps (Internal App ↔ Internal App)

## 🌐 1. [Initial Enumeration](../../starting_point/2_initial-steps.md)

## 🔍 1. Confirm Port Accessibility

```bash
nmap -p 22 -sV -Pn <target_ip>
```
- `-p 22`: Scan port 22
- `-sV`: Service version detection

**Look for:**  
- SSH banners (version, vendor)
- Unexpected services running on 22

**Click Below If...**
- [ ] [Target Port is Filtered](../restrictions/nmap_state_filtered.md)

---

## 🔍 2. Grab SSH Banner

```bash
nc <target_ip> 22
```
or

```bash
telnet <target_ip> 22
```
**Expected output:**  
- SSH version (`SSH-2.0-OpenSSH_8.4` or similar)
- Sometimes includes OS fingerprint leaks.

---

## 🔍 3. Deep Version and Configuration Scanning

```bash
nmap -p22 --script ssh2-enum-algos,ssh-hostkey,ssh-auth-methods <target_ip>
```
**Scripts explanation:**
- `ssh2-enum-algos`: Lists supported algorithms (ciphers, MACs, key exchanges)
- `ssh-hostkey`: Fetches SSH host key fingerprint (can be reused to find clones)
- `ssh-auth-methods`: Checks supported authentication methods (password, publickey)

---

## 🔍 4. Check for Bruteforce Potential (Carefully!)

```bash
hydra -l <username> -P <password_list.txt> ssh://<target_ip>
```
- Only perform if **explicitly authorized**.  
- Used to detect weak/default credentials.

---

# 💥 Port 22 Exploitation Steps (Internal App ↔ Internal App)

## ⚡ 1. Attempt Default or Guessable Credentials

Example manual login attempts:

```bash
ssh user@<target_ip>
```
Try commonly used usernames like:
- `admin`
- `deploy`
- `developer`
- `root` (sometimes disabled but worth checking internally)

---

## ⚡ 2. Exploit Weak SSH Configurations

**Look for:**
- Outdated SSH versions (CVE-prone)
- Weak cipher usage (e.g., deprecated algorithms like `diffie-hellman-group1-sha1`)
- Absence of key-based authentication enforcement

**Nmap NSE scripts can help confirm this:**

```bash
nmap --script sshv1,ssh2-enum-algos -p22 <target_ip>
```

---

## ⚡ 3. Check for SSH Tunneling Abuse

If an internal app allows **SSH port forwarding** without restriction:

```bash
ssh -L <local_port>:<target_internal_service>:<target_internal_port> user@<target_ip>
```

Example:  
Tunnel database access through the SSH session, effectively pivoting inside the cloud environment.

---

## ⚡ 4. Abuse SSH Agent Forwarding (If Misconfigured)

If internal apps connect using agent forwarding and `ForwardAgent yes` is insecurely set:

- **Hijack SSH agent** → **Use it to authenticate elsewhere** inside the cloud.

Detection:

```bash
echo $SSH_AUTH_SOCK
ssh-add -l
```

If agent forwarding is active, and another app uses the same SSH connection, it could be abused.

---

# 🧠 Quick Security Notes

| Misconfiguration         | Risk                              |
|---------------------------|-----------------------------------|
| Default/Weak Credentials  | Full compromise                  |
| Outdated SSH version      | RCE, key recovery vulnerabilities |
| Agent Forwarding           | Credential theft, lateral movement |
| Weak Ciphers              | Traffic decryption, session hijack |

---

# 📋 Recommendations

- **Enforce key-based authentication** (no passwords).
- **Disable agent forwarding** unless absolutely necessary.
- **Use strong ciphers and updated SSH versions**.
- **Restrict internal app SSH access by IP and user roles**.
- **Implement idle session timeouts**.