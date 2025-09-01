Bandit Level 1 → 2

Goal:
- Retrieve the password for Level 2.
- The password is stored in a file named 'spaces in this filename' in the home directory of Level 1.

Steps:
1. Log in as bandit1 (Level 1) via SSH.
2. List files in the home directory to see the exact filename:
   ls
   # Output: 'spaces in this filename'
3. Display the contents of the file:
   cat "spaces in this filename"

Result:
- The file contains the password for Level 2.
- In this repo, the password is **blurred for security** in screenshots.

Screenshot:
- [Add screenshot here showing the command used to cat the file]
- The screenshot shows the command; password is blurred.
