### Bandit Level 25 → Level 26

#### **Goal**

Log in to Bandit 26, whose shell is not a standard `/bin/bash` but a restricted shell. The objective is to figure out the nature of the restricted shell and "break out" of it to gain a regular shell.

#### **Commands**

`ssh`

-----

### **Walkthrough**

1.  **Attempt to log in to Bandit 26**: First, try to log in to `bandit26` using the password you obtained from the previous level.

    ```bash
    bandit25@bandit:~$ ssh bandit26@localhost -p 2220
    ```

    Upon successful login, you'll be greeted by a message and a prompt that doesn't behave like a normal bash shell. The shell appears to be a custom program that only accepts a limited number of inputs. Typing anything other than a specific command will likely result in a message like "This is a restricted shell."

2.  **Examine the Shell's Behavior**: The prompt will probably show something like `ls`. If you type `ls`, it will list the files in the current directory. However, if you try to use any other command, such as `cat`, you'll get an error message. The shell is designed to only allow the `ls` command to be run.

3.  **Break Out of the Restricted Shell**: The key to this level is to find a way to escape the restricted shell and get a full `bash` shell. In many restricted shells, if a command expects input from the user (like `ls` often does) and you provide it with an argument that starts with a hyphen (`-`), the shell may pass it directly to the underlying program. This can be exploited to get unexpected behavior.

      * Try typing `ls -a` to see if it allows you to pass an argument. It likely will.
      * The secret to this level is to exploit the input handling. If you type the `ls` command followed by a semicolon `;` and then the command for the shell you want to run, you can often bypass the restriction. The semicolon is a command separator in many shells, allowing you to chain commands together. Try the following:

    <!-- end list -->

    ```bash
    ls ; /bin/bash
    ```

    This command will first run `ls`, which is allowed, and then execute `/bin/bash`, which will give you a full, unrestricted shell. You will then have a regular prompt for the `bandit26` user.

4.  **Find the Password**: Once you have a regular shell, you can use standard commands to find the password for `bandit27`. The password will be in the `/etc/bandit_pass/bandit26` file.

    ```bash
    bandit26@bandit:~$ cat /etc/bandit_pass/bandit26
    ```
**Screenshot for refference**
![](screenshots/command.png)
