Bandit Level 5 → Level 6
------------------------
Goal: Find the password for the next level.

Clues:
- Human-readable
- 1033 bytes
- Not executable

Steps and Explanations:

1. Go into the inhere directory:
   cd inhere
   # All candidate files are under this directory.

2. Locate the file of the correct size and type:
   find . -type f -size 1033c ! -executable -exec file {} \; | grep "ASCII text"
   # Explanation:
   # - `find .` searches recursively in the current directory.
   # - `-type f` ensures we only look for regular files.
   # - `-size 1033c` looks for files exactly 1033 bytes (c = bytes).
   # - `! -executable` excludes executable files.
   # - `-exec file {} \;` runs `file` on each candidate to determine its type.
   # - `grep "ASCII text"` filters for human-readable files.

3. Enter the directory containing the file and list hidden files:
   cd maybehere07
   ls -a
   # Explanation:
   # - Some files start with a `.` and are hidden, so normal `ls` won't show them.
   # - `ls -a` lists all files including hidden ones.

4. Print the content of the hidden file:
   cat .file2
   # Explanation:
   # - Only `.file2` is the correct file (found from step 2).
   # - `cat` outputs its contents to the terminal to reveal the password.
   # - We must include the `.` because it's part of the hidden filename.

Level 5 → 6 Password
Password is blurred for reference

Output Screenshot:
![Bandit Level 5 → 6 Output](screenshots/command.png)
