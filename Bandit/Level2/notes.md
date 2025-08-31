# Bandit Level 2 → 3

## Level Goal
The password for the next level is stored in a file called `--spaces in this filename--`.

---

## Steps

1. **Login to Bandit2**  
   ssh bandit2@bandit.labs.overthewire.org -p 2220  
   *(Use the password from Level 1 → 2)*  

   ![SSH Login](sshlogin.png)

2. **List files in the home directory**  
   ls -lb  
   This shows a file named `--spaces in this filename--`.

3. **Read the contents of the file**  
   cat -- "--spaces in this filename--"  
   The command prints the password for **Level 3**.  
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx(passwords might vary as OTW updates or changes them please follow up practically)

   ![Commands Output](command.png)

---

## Result
The password found in the file is used to log in to **Bandit Level 3**.
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
