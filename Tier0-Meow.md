# HTB: Meow (Tier 0)

## 📍 Info
- Difficulty: Easy
- Skills: Telnet, basic recon
- My Rating: ⭐️

## 🔎 Recon
```bash
nmap -sV -p- 10.10.x.x

#🚪 Exploitation
```bash
telnet 10.10.x.x 23

📚 What I Learned
Telnet = wide open if not secured

First exposure to command-line hacking

**`add Meow writeup`**

3. Scroll down, write a commit message:  
   **`add Meow writeup`**  
4. Click **Commit new file**

BAM 💥 — your first public cyber writeup is LIVE.

---

## 🔗 STEP 4: Share or Build on It

- Share the repo link on your LinkedIn, resume, or Notion when you’re ready
- Keep adding markdown files: `Fawn.md`, `Oopsie.md`, `Tier1-Appointment.md`
- Add a table of contents to the README later

---

## 🧠 OPTIONAL: Make It Cleaner (Pro tips)

In your README, you can start organizing like:

```markdown
# 🧠 HTB Writeups

Welcome to my personal writeups and notes as I go through Hack The Box labs.

## ✅ Tier 0
- [Meow](./Tier0-Meow.md)
- [Fawn](./Tier0-Fawn.md)

## 🔓 Tier 1
- [Dancing](./Tier1-Dancing.md)
- [Oopsie](./Tier1-Oopsie.md)


