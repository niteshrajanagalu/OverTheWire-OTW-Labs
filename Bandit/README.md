# OverTheWire: Bandit

The **Bandit wargame** teaches the fundamentals of working with Linux, the command line, and basic networking.  
Each level is designed as a puzzle that introduces new commands and concepts frequently used in cybersecurity.

---

## 🔑 Connecting to Bandit

Use SSH to connect to the game server:

```bash
ssh banditX@bandit.labs.overthewire.org -p 2220
```

- Replace `X` with the level number (e.g., `bandit0`, `bandit5`, etc.).  
- The password for each level is either provided or obtained from the previous level.  

---

## 📂 Repository Structure

This folder contains my notes for each Bandit level.  
Each subfolder corresponds to a level transition (e.g., **Level 0 → Level 1**).  

```
bandit/
├── README.md
├── 01_Level0/
├── 02_Level0-1/
├── 03_Level1-2/
├── 04_Level2-3/
...
├── 34_Level32-33/
└── FINAL LEVEL/
```

---

## 📘 Levels Overview

Click below to view notes for each level:

- [01_Level0](./01_Level0/) → Connecting with SSH  
- [02_Level0-1](./02_Level0-1/) → Reading files  
- [03_Level1-2](./03_Level1-2/) → Hidden files  
- [04_Level2-3](./04_Level2-3/) → File types  
- [05_Level3-4](./05_Level3-4/) → Searching for files  
- [06_Level4-5](./06_Level4-5/) → File search by size/permissions  
- [07_Level5-6](./07_Level5-6/) → Advanced `find` usage  
- [08_Level6-7](./08_Level6-7/) → Using `grep`  
- [09_Level7-8](./09_Level7-8/) → Unique lines  
- [10_Level8-9](./10_Level8-9/) → Extracting strings  
- [11_Level9-10](./11_Level9-10/) → Base64 decoding  
- [12_Level10-11](./12_Level10-11/) → ROT13 decoding  
- [13_Level11-12](./13_Level11-12/) → Working with compressed files  
- [14_Level12-13](./14_Level12-13/) → SSH private keys  
- [15_Level13-14](./15_Level13-14/) → Password storage in `/etc/bandit_pass`  
- [16_Level14-15](./16_Level14-15/) → SSL with `openssl s_client`  
- [17_Level15-16](./17_Level15-16/) → Port scanning with `nmap`  
- [18_Level16-17](./18_Level16-17/) → File comparison with `diff`  
- [19_Level17-18](./19_Level17-18/) → `.bashrc` tricks  
- [20_Level18-19](./20_Level18-19/) → SUID binaries  
- [21_Level19-20](./21_Level19-20/) → Netcat and setuid validation  
- [22_Level20-21](./22_Level20-21/) → Cron jobs  
- [23_Level21-22](./23_Level21-22/) → Cron with scripts  
- [24_Level22-23](./24_Level22-23/) → More cron automation  
- [25_Level23-24](./25_Level23-24/) → Brute force scripting  
- [26_Level24-25](./26_Level24-25/) → Restricted shell escapes  
- [27_Level25-26](./27_Level25-26/) → Advanced SSH usage  
- [28_Level26-27](./28_Level26-27/) → Git basics  
- [29_Level27-28](./29_Level27-28/) → Git branching  
- [30_Level28-29](./30_Level28-29/) → Git tags  
- [31_Level29-30](./31_Level29-30/) → Inspecting Git commits  
- [32_Level30-31](./32_Level30-31/) → Git rebase  
- [33_Level31-32](./33_Level31-32/) → Command injection  
- [34_Level32-33](./34_Level32-33/) → Final challenge setup  
- [FINAL LEVEL](./FINAL%20LEVEL/) → End of Bandit

---

## 📝 Notes

- Notes are written for **educational purposes**.  
- The focus is on **commands, problem-solving steps, and lessons learned**.  
- This builds a personal **cybersecurity knowledge base** for CTFs and real-world tasks.  

---

🚀 **Next Steps:** After Bandit, try **Krypton (crypto basics)**, **Leviathan (binary exploitation basics)**, and **Natas (web security)**.
