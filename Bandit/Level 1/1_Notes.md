# Bandit Level 1 → 2 Notes
#Goal
Connect to the Bandit server using SSH and retrieve the password for Level 2.

---

 Steps Taken

1. **SSH into the server**

ssh bandit1@bandit.labs.overthewire.org -p 2220

 Password: (from Level 0 solution)
 Connected successfully.

![SSH Connection](screenshots/1_sshlevel1.png)

---

2. **List files and find the password**

* Checked the contents of the home directory:
ls
ls command lists all the contents of the current directory(Home)
* Found a file named "-"

* Viewed the contents of the file to get the password:

cat ./-
Here ./ refers to the current directory and ensures that the file named "-" is treated as a normal file instead of stdin/stdout.
![Commands and Output](2_screenshots/2_catpassword.png)

## Solution / Password for Level 2
263JGJPfgU6LtdEvgfWU1XP5yac29mFx

## Important Note
- If a file has tricky names like "-" use ./filename or quotes.
- Always check the home directory first for files.
- Screenshots help remember SSH connections and commands used.
