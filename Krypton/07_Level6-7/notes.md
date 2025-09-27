# Krypton: Level 6 → Level 7

This level's challenge is to break a **stream cipher** by performing a **known-plaintext attack**. The cipher's weakness is its pseudo-random number generator, an **8-bit LFSR**, which produces a short, repeating keystream. Our strategy is to reveal this keystream and use it to decrypt the password.

-----

## 🔎 Walkthrough from Screenshots

### 1\. Initial Analysis & Setup

First, we navigate to the challenge directory `/krypton/krypton6` and gather intelligence by reading the hint files.

  * **HINT1** reveals the generator is periodic.
  * **HINT2** confirms the specific vulnerability: an **8-bit LFSR**.

It's good practice to create a separate working directory in `/tmp` to avoid cluttering the original challenge folder. We then create symbolic links (`ln -s`) to the necessary files (`encrypt6`, `krypton7`, `keyfile.dat`) so we can work with them from our new location.

```bash
krypton6@krypton:/krypton/krypton6$ mkdir /tmp/lvl7
krypton6@krypton:/krypton/krypton6$ cd /tmp/lvl7
krypton6@krypton:/tmp/lvl7$ ln -s /krypton/krypton6/encrypt6
krypton6@krypton:/tmp/lvl7$ ln -s /krypton/krypton6/krypton7
```

### 2\. The Known-Plaintext Attack

Inside our workspace (`/tmp/lvl7`), we create a file, `a.txt`, containing a long string of a single character ('A'). We then run the linked `encrypt6` executable, using `a.txt` as the plaintext to generate `cipher.txt`.

```bash
# Create a file with a long string of 'A's
krypton6@krypton:/tmp/lvl7$ python -c "print('A'*100)" > a.txt

# Encrypt the known plaintext
krypton6@krypton:/tmp/lvl7$ ./encrypt6 a.txt cipher.txt
```

### 3\. Finding the Key with Sublime Text

We `cat` the resulting `cipher.txt` and copy its output. By pasting this string into a local text editor like **Sublime Text**, we can easily add line breaks and visually identify the repeating pattern. This pattern is the cipher's key.

The repeating key is: **`EICTDGYIYZKTHNSIRFXYCPFUEOCKRN`**

### 4\. Transferring the Decoder Script

From our local Kali machine, we use the **`scp` (Secure Copy)** command to upload our `vignere_decoder.py` script to the `/tmp/lvl7` directory on the remote server.

```bash
(ethos@kali)-[~]
└─$ scp -P 2231 vignere_decoder.py krypton6@krypton.labs.overthewire.org:/tmp/lvl7
```

### 5\. Decrypting the Password

With the key identified and the decoder script in our workspace, we can execute the final command to decrypt the password file.

```bash
krypton6@krypton:/tmp/lvl7$ python3 vignere_decoder.py krypton7 EICTDGYIYZKTHNSIRFXYCPFUEOCKRN
```

-----

## 🔑 Password for Level 7

The decrypted password is: **`LFSRISNOTRANDOM`**

-----

## 🐍 Appendix: `vignere_decoder.py` Script

\<details\>
\<summary\>Click to view the Python code used for decryption.\</summary\>

```python
#!/usr/bin/python3

# Script by NITESH

import sys

key = ""
alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

if __name__=="__main__":

    out_string = ""

    if (len(sys.argv)) != 3:
        print("Usage: python3 vignere_decoder.py filename key")
        exit(0)
    else:

        key = sys.argv[2]

        print("Decoding file '" + sys.argv[1] + "' with key '" + sys.argv[2] + "':\n")

        try:
            with open(sys.argv[1]) as fh:
                lines = fh.readlines()
        except:
            print("No file named '" + sys.argv[1] + "'")
            exit(0)

        for line in lines:
            line = line.replace(" ", "")
            line = line.replace("\n", "")
            for index in range(len(line)):
                c = alphabet[(alphabet.index(line[index]) - alphabet.index(key[index % len(key)])) % 26]
                out_string += c

    print(out_string)
```

\</details\>

