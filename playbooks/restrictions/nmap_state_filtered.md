# 🚧 What to Do if Port Shows as "Filtered" in Nmap

When you run:

```bash
nmap -p <port> -sV -Pn <target_ip>
```

and **state = filtered**, it means:

| Term         | Meaning                                                  |
|--------------|-----------------------------------------------------------|
| **Filtered** | Nmap cannot tell if the port is open because a firewall or security device is silently dropping the packets. |

**In short:**  
> The packets are being blocked before they reach the SSH service.

---

# 🔍 Steps to Handle Filtered Port 22

## 1. Try Different Scan Techniques

> **Goal:** Figure out if a firewall is blocking or just "hiding" the port.

- **TCP SYN Scan (Stealthier):**

```bash
sudo nmap -p 22 -sS -Pn <target_ip>
```
- **TCP Connect Scan (Full TCP handshake):**

| Scan Type       | if Result    | Meaning                                        |
|-----------------|-----------|------------------------------------------------|
| SYN (-sS)       | filtered  | Firewall silently dropping SYNs                |

```bash
nmap -p 22 -sT -Pn <target_ip>
```
- **TCP ACK Scan (Firewall Detection):**

| Scan Type       | if Result    | Meaning                                        |
|-----------------|-----------|------------------------------------------------|
| Connect (-sT)   | filtered  | TCP connection blocked or dropped              |

```bash
nmap -p 22 -sA -Pn <target_ip>
```
| Scan Type       | if Result    | Meaning                                        |
|-----------------|-----------|------------------------------------------------|
| ACK (-sA)       | filtered  | No response = stateful firewall or deep packet inspection |

---

## 2. Scan Over Different Source Ports

Sometimes firewalls allow certain trusted ports (like 80 or 443) but block 22.

- **Spoof Source Port 443:**

```bash
nmap -p22 -g 443 -Pn <target_ip>
```
- **Spoof Source Port 80:**

```bash
nmap -p22 -g 80 -Pn <target_ip>
```
> `-g`: Set source port to bypass naive firewall rules.

---

## 3. Use Timing and Fragmentation Evasion Techniques

Firewalls might drop standard nmap probes but not fragmented/slow ones.

- **Fragment Packets:**

```bash
nmap -p22 -sS -f -Pn <target_ip>
```

- **Slow Down (Timing Option):**

```bash
nmap -p22 -sS -T2 -Pn <target_ip>
```
> `-f`: Fragment packets.  
> `-T2`: Slow down scan to look "less suspicious."

---

## 4. Check for ICMP Filtering

Verify if the entire host is "hardened" or unreachable at the network layer:

```bash
ping <target_ip>
```

If no ping reply, it doesn't necessarily mean it's down — just **ICMP Echo Requests** are filtered too.

---

## 5. Analyze Firewall Behavior

Run a broader firewall detection scan:

```bash
nmap -p22 --script firewalk,firewall-bypass -Pn <target_ip>
```
- `firewalk`: Attempts to identify firewall/router ACLs.
- `firewall-bypass`: Attempts to circumvent simple firewalls.

---

# 🧠 Interpretation Cheat Sheet

| Situation                     | What It Likely Means                  |
|--------------------------------|----------------------------------------|
| No response at all             | Packet dropped by firewall            |
| TCP RST (reset) response       | Port closed, but host reachable       |
| TCP SYN-ACK or SSH banner seen | Port open                             |
| ICMP unreachable               | Host/router filtering packets         |

---

# 📋 Final Thoughts

If you **cannot bypass the filtering**, note it as a **finding** in your AppSec report:

> "**SSH (Port 22) is filtered between internal applications, preventing unauthorized remote access. Firewall filtering is correctly enforced at the network layer.**"

**✅** This is actually a **good** security control for internal applications.