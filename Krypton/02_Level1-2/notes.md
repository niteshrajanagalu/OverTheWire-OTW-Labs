# Krypton Level 1 → Level 2 Notes
**Level:** 1 → 2  
**Goal:** Obtain the password for Level 2

## Level Summary
- The password for Level 2 is in the file: `krypton2`  
- The content is **encrypted using ROT13**, a simple letter rotation cipher.  
- ROT13 shifts letters 13 positions in the alphabet (A→N, N→A, etc.).  
- Spaces and punctuation remain unchanged.  

## Steps to Solve

### 1️⃣ Navigate to the level directory
```bash
cd /krypton/krypton1
ls
```

### 2️⃣ View encrypted content
```bash
cat krypton2
# Output: YRIRY GJB CNFFJBEQ EBGGRA
```

### 3️⃣ Decrypt using ROT13
```bash
cat krypton2 | tr 'A-Za-z' 'N-ZA-Mn-za-m'
# Output: LEVEL TWO PASSWORD ROTTEN
```

### 4️⃣ Password
```
LEVEL TWO PASSWORD ROTTEN
```

### 5️⃣ Login to Level 2
```bash
ssh krypton2@<host>
# Enter password: LEVEL TWO PASSWORD ROTTEN
```

## Hints / Notes
* ROT13 is symmetric; applying it twice restores the original text.  
* Spaces and punctuation are not affected.  
* `cd /krypton/krypton1` ensures you are in the correct directory.  
* Understanding ROT13: mentally split the alphabet in half (A–M / N–Z); swap halves to decode.
