Bandit OTW Notes – Level 13 to 14

Goal: Log in to Bandit14 using a private SSH key.
- The next password is not given directly.
- Bandit13 provides a private key file to access Bandit14.

Steps:

1. Locate the private key file in your home directory:
ls -l
Example output:
-rw-r----- 1 bandit14 bandit13 1679 Aug 15 13:15 sshkey.private

2. SSH into Bandit14 using the key:
ssh -i sshkey.private bandit14@localhost -p 2220

Screenshot reference: command.png

3. Retrieve the Bandit15 password from Bandit14:
cat /path/to/password_file

Screenshot reference: command1.png

Notes:
- /etc/bandit_pass/bandit14 is not directly readable; the key file acts as the login credential.
- Permissions (chmod 600) on the key are not required if you can read the file.
- The password for Bandit15 is obtained via the provided file or program in Bandit14.
