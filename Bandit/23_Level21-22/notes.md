### Bandit Level 21 → Level 22 Walkthrough

This level requires you to inspect a cron job to find the password for the next level. **Cron** is a time-based job scheduler in Unix-like operating systems. It allows users to schedule commands or scripts to run automatically at specified intervals.

-----

### Step-by-Step Guide

1.  **Locate the Cron Job Configuration**: The level description tells you to look in the `/etc/cron.d/` directory. This directory holds system-wide cron jobs. Use the `ls -la /etc/cron.d/` command to list the files in this directory and find the one related to the `bandit22` user.

    ```bash
    bandit21@bandit:~$ ls -la /etc/cron.d/
    ```

2.  **Examine the Cron Job File**: Once you identify the file, use the `cat` command to view its contents. The file will likely be named `cronjob_bandit22` or something similar.

    ```bash
    bandit21@bandit:~$ cat /etc/cron.d/cronjob_bandit22
    ```

    The output will show the cron job entry, which typically looks like this:

    ```
    * * * * * bandit22 /usr/bin/cronjob_bandit22.sh &> /dev/null
    ```

    This line indicates that the script `/usr/bin/cronjob_bandit22.sh` is executed every minute by the `bandit22` user. The `&> /dev/null` part redirects both standard output and standard error to `/dev/null`, meaning you won't see any output on the screen.

3.  **Inspect the Script**: Now, you need to see what the script `/usr/bin/cronjob_bandit22.sh` does. Use the `cat` command again to view the script's contents.

    ```bash
    bandit21@bandit:~$ cat /usr/bin/cronjob_bandit22.sh
    ```

    The script's content will reveal how the password is being stored. It likely looks like this:

    ```bash
    #!/bin/bash
    chmod 644 /tmp/t70I6lds95QORqQh9AcmcZ6ShpAoZK7fgv
    cat /etc/bandit_pass/bandit22 > /tmp/t70I6lds95QORqQh9AcmcZ6ShpAoZK7fgv
    ```

    The first line `chmod 644 ...` sets the permissions of a file. The second line `cat /etc/bandit_pass/bandit22 > /tmp/t70I6lds95QORqQh9AcmcZ6ShpAoZK7fgv` is the key. It copies the contents of the password file `/etc/bandit_pass/bandit22` into a temporary file in the `/tmp/` directory. The filename is unique and randomly generated each time, as shown in the output from the image.

4.  **Retrieve the Password**: The password is being written to a file in the `/tmp/` directory. You can use the `ls -la /tmp/` command to find this file. The `ls` command will show you a file that starts with `t70` and has the `644` permissions.

    ```bash
    bandit21@bandit:~$ ls -la /tmp/
    ```

    Once you have the filename, use `cat` to read its contents.

    ```bash
    bandit21@bandit:~$ cat /tmp/t70I6lds95QORqQh9AcmcZ6ShpAoZK7fgv
    ```

    This command will display the password for the next level.

5.  **Use the Password to Log In**: Use the retrieved password to log in to the next level.

    ```bash
    bandit22@bandit:~$
    ```

-----

### Professional GitHub Notes

## Bandit Wargame: Level 21 → Level 22 Walkthrough

### 🎯 Level Goal

The objective of this level is to find the password for **Bandit Level 22** by analyzing a **cron job**. A cron job is a scheduled task that runs automatically on a Unix-like system. The problem description hints that the cron configuration is located in the `/etc/cron.d/` directory.

### 💡 Methodology

1.  **Locate the Cron Job**: First, list the contents of the `/etc/cron.d/` directory to identify the relevant cron job file.
2.  **Inspect the Cron Job**: Read the contents of the identified file to understand what command or script is being executed.
3.  **Analyze the Script**: The cron job points to a shell script. Inspect this script to see how it handles the password. The script will reveal where the password is being stored or what is being done with it.
4.  **Retrieve the Password**: The password is being redirected to a temporary file in the `/tmp/` directory. The script reveals the name of this file. Use the `cat` command to read the contents of this temporary file and retrieve the password.

### 💻 Commands Used

Here's the sequence of commands used to solve this level:

| Command | Purpose |
| :--- | :--- |
| `ls -la /etc/cron.d/` | List all files in the directory containing the system cron jobs. |
| `cat /etc/cron.d/cronjob_bandit22` | Display the contents of the cron job file for `bandit22`. This reveals the path to the script being run. |
| `cat /usr/bin/cronjob_bandit22.sh` | Show the source code of the script. This is where we learn that the password is being copied to a temporary file. |
| `ls -la /tmp/` | List files in the `/tmp/` directory to find the temporary file. |
| `cat /tmp/t70I6lds95QORqQh9AcmcZ6ShpAoZK7fgv` | Read the contents of the temporary file to get the password. |

### 📸 Screenshot

Here's a screenshot showing the key commands used to solve the level:

\!
**Image Path**: `screenshots/command.png`

### ✅ Solution

The password for Bandit Level 22 is found in a temporary file in the `/tmp/` directory. The filename is a random string generated by the script `/usr/bin/cronjob_bandit22.sh`. The final command to retrieve the password is `cat /tmp/t70I6lds95QORqQh9AcmcZ6ShpAoZK7fgv`.
