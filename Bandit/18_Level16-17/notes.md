Bandit Level 16 → Level 17  

Level Goal:  
Instead of a password, the correct port will return an RSA private key. This private key is used to log into the next level.  

Step-by-Step Approach:  

1. Scan ports 31000–32000 for open services:  
```
nmap -p 31000-32000 localhost
```

![Nmap Scan](screenshots/command1.png)

Open ports found: `31046, 31518, 31691, 31790, 31960`

2. Pipe the Bandit16 password into each open port using SSL:  
```
for port in 31046 31518 31691 31790 31960; do
    echo "kSkvUpMQ7lBYyCM4GBPvCvT1BfWRy0Dx" | ncat --ssl localhost $port
done
```

3. Only port **31790** returned the RSA private key:  
```
Port: 31790
Correct!
-----BEGIN RSA PRIVATE KEY-----
[...private key...]
-----END RSA PRIVATE KEY-----
```

![Private Key Found](screenshots/command.png)

4. Save the RSA key into a file and set proper permissions:  
```
nano bandit17.key
chmod 600 bandit17.key
```

5. Use the key to log in to the next level:  
```
ssh -i bandit17.key bandit17@bandit.labs.overthewire.org -p 2220
```

You are now logged into **Bandit17**.
