### 🔐 Bandit Level 25 → 26: CTF Wargame Walkthrough

This level is tricky because the `bandit26` user's default shell isn't a standard, interactive one. Instead of a password, you're given an SSH key to log in. The core challenge is getting a proper shell to find the password for the next level.

-----

### **Step 1: Get the SSH Key onto Your Local Machine**

You can't directly use the `bandit26.sshkey` from within the `bandit25` shell, and you might not have the permissions to copy it to a location like `/tmp/`. The most reliable way to handle this is to copy the key's contents manually.

1.  **View the key's content:** From the `bandit25` shell, use `cat` to print the key's contents to your terminal.
    ```bash
    bandit25@bandit:~$ cat bandit26.sshkey
    ```
2.  **Copy the key:** Select and copy the entire block of text, from `-----BEGIN OPENSSH PRIVATE KEY-----` to `-----END OPENSSH PRIVATE KEY-----`.
3.  **Create the file on your local machine:** On your local machine (e.g., your Kali terminal), create a new file named `bandit26.key`. You can use a text editor like `nano`.
    ```bash
    $ nano bandit26.key
    ```
    Paste the copied text into the file and save it.

-----

### **Step 2: Set the Correct Permissions**

SSH requires private key files to have very strict permissions for security. You must change the file's permissions to `600`, which means only you (the file owner) can read and write to it.

```bash
$ chmod 600 bandit26.key
```

  * **chmod**: The command to change file permissions.
  * **600**: The numeric permission code:
      * **6** (read and write) for the owner.
      * **0** (no permissions) for the group.
      * **0** (no permissions) for others.
  * **bandit26.key**: The name of the key file.

-----

### **Step 3: Connect and Break Out of the Restricted Shell**

When you connect to Bandit 26, the default shell is a program that just displays a banner and then exits. To get a working shell, you need to tell SSH to run a different command immediately upon login.

1.  **Connect with a specified shell:** Use the `-i` flag to specify your key and, at the end of the command, provide the path to a standard shell like `/bin/bash` or `/bin/sh`. This will be executed on the remote server after a successful authentication.
    ```bash
    $ ssh bandit26@bandit.labs.overthewire.org -i bandit26.key -p 2220 /bin/bash
    ```
      * **-i**: Specifies the identity file (your key).
      * **-p**: Specifies the port number.
      * **/bin/bash**: The command to execute after logging in.

-----

### **Step 4: Find the Password**

Once you have a proper shell, the password for the next level is in a file in the current directory.

1.  **List files**: Use `ls -la` to view all files, including hidden ones, in the current directory.
    ```bash
    bandit26@bandit:~$ ls -la
    ```
2.  **Read the password**: You'll find a file named `bandit27-password`. Use `cat` to read its contents.
    ```bash
    bandit26@bandit:~$ cat bandit27-password

![](screenshots/command.png)
    ```
