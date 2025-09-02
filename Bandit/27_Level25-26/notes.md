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


      * Try typing `ls -a`  you will see sshkey

    <!-- end list -->

    ```bash
    cat sshkey
    ```


    ```bash
    bandit26@bandit:~$ Password for your next level will be displayed
    ```
**Screenshot for refference**
![](screenshots/command.png)
