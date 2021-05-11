# Notes for the Room Encryption - Crypto 101 (https://tryhackme.com/room/encryptioncrypto101)

## Tasks:

### Task 2

Are SSH keys protected with a passphrase or a password?

```
passphrase
```

### Task 3

What does SSH stand for?

```
Secure Shell
```

How do webservers prove their identity?

```
certificates
```

What is the main set of standards you need to comply with if you store or process payment card details?

```
PCI-DSS
```

### Task 4

What's 30 % 5?

```
0
```

What's 25 % 7

```
4
```

What's 118613842 % 9091

```
3565
```

### Task 5

Should you trust DES? Yea/Nay

```
Nay
```

What was the result of the attempt to make DES more secure so that it could be used for longer?

```
Triple DES
```

Is it ok to share your public key? Yea/Nay

```
Yea
```

### Task 6

p = 4391, q = 6659. What is n?

```
29239669
```

### Task 8

What company is TryHackMe's certificate issued to?

```
Cloudflare
```

### Task 9 

What algorithm does the key use?

```
RSA
```

Crack the password with John The Ripper and rockyou, what's the passphrase for the key?

```
python /usr/share/john/ssh2john.py id_rsa > id_rsa_hash.txt

┌──(kali㉿kali)-[~/THM/rooms/ENcryption_Crypto_101]
└─$ john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 4 OpenMP threads
Note: This format may emit false positives, so it will keep trying even after
finding a possible candidate.
Press 'q' or Ctrl-C to abort, almost any other key for status
delicious        (id_rsa)
Warning: Only 2 candidates left, minimum 4 needed for performance.
1g 0:00:00:04 DONE (2021-05-11 03:31) 0.2487g/s 3567Kp/s 3567Kc/s 3567KC/sa6_123..*7¡Vamos!
Session completed
```

### Task 11

 You have the private key, and a file encrypted with the public key. Decrypt the file. What's the secret word?

```
$ gpg --import tryhackme.key 
gpg: /home/kali/.gnupg/trustdb.gpg: trustdb created
gpg: key FFA4B5252BAEB2E6: public key "TryHackMe (Example Key)" imported
gpg: key FFA4B5252BAEB2E6: secret key imported
gpg: Total number processed: 1
gpg:               imported: 1
gpg:       secret keys read: 1
gpg:   secret keys imported: 1

$ gpg -d message.gpg    
gpg: encrypted with 1024-bit RSA key, ID 2A0A5FDC5081B1C5, created 2020-06-30
      "TryHackMe (Example Key)"
You decrypted the file!
The secret word is Pineapple.

```

