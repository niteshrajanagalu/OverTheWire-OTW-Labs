# OverTheWire: Krypton Level 3 → 4 Walkthrough

This level moves beyond a simple substitution cipher. We are given four ciphertext files (`krypton4`, `found1`, `found2`, `found3`) and told they were all encrypted using the same key. This suggests a polyalphabetic cipher, likely a Vigenère cipher.

The strategy is to combine all the ciphertext files into one large text. This gives us a bigger sample size, which makes **frequency analysis** much more effective for cracking the key.

-----

## Step 1: Setup and Tools

First, I created a temporary directory on the server to keep the files organized. I then needed a tool to perform frequency analysis. I wrote a simple Python script, `freq_analysis.py`, to count the occurrences of single characters (monograms), pairs (digrams), and triplets (trigrams).

I transferred this script from my local machine to the remote server using `scp`.

```bash
# Command to transfer the script
scp -P 2231 freq_analysis.py krypton3@krypton.labs.overthewire.org:/tmp/tmp.nBvIecuVca
```
## REFERENCE SCREENSHOT:
![](/screenshots/scp.png)
Here is the Python script used for the analysis. It takes a filename and a group size (e.g., 1 for monograms, 3 for trigrams) as arguments.



## Step 2: Performing Frequency Analysis

The core of this challenge is frequency analysis. The principle is that in any language, some letters and letter combinations appear more often than others. In English, 'E' is the most common letter, and 'THE' is the most common three-letter word (trigram).

I ran the script first with a group size of **1** to find the most common single letters.

Then, I ran it with a group size of **3** to find the most common trigrams. This is often the key to breaking this type of cipher. The analysis showed that **`JDS`** was the most frequent trigram in the combined ciphertext.

-----
## REFERENCE SCREENSHOT:Group size 1 and 2
![](/screenshots/command1.png)

## Group Size 2
![](/screenshots/comman2.png)

## Step 3: Iterative Decryption

My working hypothesis was that the most common ciphertext trigram, `JDS`, corresponds to the most common English trigram, `THE`.

I used the `tr` command to substitute these characters and slowly reveal the plaintext. I started with `JDS` -\> `THE` and then used the partially decrypted text to make more educated guesses.

## SCREENSHOT REFERENCE:
![](/screenshots/command3.png)


This was an iterative process:

1.  Make a substitution.
2.  Observe the output for recognizable words or patterns.
3.  Guess the next substitution based on the new context.
4.  Repeat.

Here's a snapshot of my thought process during the substitutions. I used a notepad to keep track of the mappings and observe the resulting plaintext. The goal was to turn the ciphertext into readable English.

![](/screenshots/notepad.png)

The key substitutions were:

  * `JDS` → `THE`
  * `QBK` → `AOW`
  * `V` → `L`
  * `IWG` → `VDN`
  * `YUN` → `PSR`

-----

## Step 4: Finding the Password

After several iterations, the message for `krypton4` started to become clear:

`WELL DONE THE LEVEL... PASSWORD IS...`

## Final Step: Decrypting the Password (BRUTE)

The iterative decryption process using `tr` revealed most of the message, leaving us with a final fragment that read:

`... PASSWORD CS ARMTE`

Based on the context, the logical plaintext is `... PASSWORD IS BRUTE`. This educated guess is the key to solving the level.

### Password Key Correspondence

To decrypt the final ciphertext `ARMTE` into `BRUTE`, the following substitutions are required:

* Ciphertext `A` → Plaintext `B`
* Ciphertext `R` → Plaintext `R`
* Ciphertext `M` → Plaintext `U`
* Ciphertext `T` → Plaintext `T`
* Ciphertext `E` → Plaintext `E`

From this, we get two new, confirmed mappings to add to our key: **`A → B`** and **`M → U`**.

### The Polyalphabetic Clue 🕵️‍♂️

This final step reveals the true nature of the cipher. The guess requires `R → R`, `T → T`, and `E → E`. However, this creates a conflict with our established substitution key, where we already found that:

* `N` decrypts to `R`
* `J` decrypts to `T`
* `S` decrypts to `E`

In a simple (monoalphabetic) substitution, one plaintext letter can only correspond to one ciphertext letter. The fact that plaintext `R` would come from both ciphertext `N` and `R` is a logical impossibility for that cipher type.

This conflict is intentional. It's the final clue that proves we are dealing with a **polyalphabetic cipher** (like Vigenère). In such ciphers, the substitution alphabet changes throughout the message, meaning the same ciphertext letter can decrypt to different plaintext letters depending on its position.

While our `tr` command couldn't perfectly model this, it was the right tool to crack the code and reveal the final password.


![](/screenshots/notepad.png)
**The password for Krypton level 4 is BRUTE.**

