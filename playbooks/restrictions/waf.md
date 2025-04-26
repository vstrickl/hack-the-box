# Confirm if Target is Restricted by WAF 

## 🔍 WAF Detection with `wafw00f`

### ✅ **Step-by-Step Command**

```bash
wafw00f https://target-domain.com
```

---

### 🧪 **Example Output (If WAF is Detected)**

```
Checking https://target-domain.com
The site https://target-domain.com is behind a Web Application Firewall.
WAF Detected: Cloudflare (Cloudflare Inc.)
```

---

### 🚫 **Example Output (If No WAF is Detected)**

```
Checking https://target-domain.com
No WAF detected.
```

---

### 📋 **Optional Flags for More Details**

- **Verbose Output:**
  ```bash
  wafw00f -v https://target-domain.com
  ```

- **Fingerprint All Possible WAFs (aggressive mode):**
  ```bash
  wafw00f -a https://target-domain.com
  ```

---

## 🧠 Tips

- Try both `http://` and `https://` if results seem inconsistent.
- Consider scanning subdomains too: `admin.target-domain.com`, `api.target-domain.com`, etc.
- If a WAF is detected, you may want to:
  - Note the vendor (e.g., AWS WAF, Cloudflare, F5).
  - Consider evasions or avoid noisy testing during recon.