# Notes for "John The Ripper" Room.

## Tasks

### Task 4

What type of hash is hash1.txt?

Used the python script

```
MD5
```

What is the cracked value of hash1.txt?

```
└─$ john --format=Raw-MD5 --wordlist=/usr/share/wordlists/rockyou.txt first_task_hashes/hash1.txt                                              1 ⨯
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD5 [MD5 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
biscuit          (?)
1g 0:00:00:00 DONE (2021-05-06 05:34) 50.00g/s 134400p/s 134400c/s 134400C/s shamrock..nugget
Use the "--show --format=Raw-MD5" options to display all of the cracked passwords reliably
Session completed

```

What type of hash is hash2.txt?

```
SHA1
```

What is the cracked value of hash2.txt

```
─$ john --format=Raw-SHA1 --wordlist=/usr/share/wordlists/rockyou.txt first_task_hashes/hash2.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-SHA1 [SHA1 128/128 AVX 4x])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
kangeroo         (?)
1g 0:00:00:00 DONE (2021-05-06 05:37) 16.66g/s 1952Kp/s 1952Kc/s 1952KC/s kanon..kalvin1
Use the "--show --format=Raw-SHA1" options to display all of the cracked passwords reliably
Session completed

```

What type of hash is hash3.txt?

```
SHA256
```

What is the cracked value of hash3.txt

```
microphone
```

What type of hash is hash4.txt?

```
Whirlpool
```

What is the cracked value of hash4.txt

```
john --format=whirlpool --wordlist=/usr/share/wordlists/rockyou.txt first_task_hashes/hash4.txt
Using default input encoding: UTF-8
Loaded 1 password hash (whirlpool [WHIRLPOOL 32/64])
Warning: poor OpenMP scalability for this hash type, consider --fork=4
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
colossal         (?)
1g 0:00:00:00 DONE (2021-05-06 05:42) 6.250g/s 4249Kp/s 4249Kc/s 4249KC/s davita1..chata74
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

### Task 5

What do we need to set the "format" flag to, in order to crack this?

```
NT
```

What is the cracked value of this password?

```
john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt ntlm.txt                 
Using default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
mushroom         (?)
1g 0:00:00:00 DONE (2021-05-06 05:49) 100.0g/s 307200p/s 307200c/s 307200C/s lance..dangerous
Use the "--show --format=NT" options to display all of the cracked passwords reliably
Session completed
```

### Task 6

What is the root password?

```
nano local_passwd
nano local_shadow

unshadow local_passwd local_shadow > unshadowed.txt

cat unshadowed.txt 
root:$6$Ha.d5nGupBm29pYr$yugXSk24ZljLTAZZagtGwpSQhb3F2DOJtnHrvk7HI2ma4GsuioHp8sm3LJiRJpKfIf7lZQ29qgtH17Q/JDpYM/:0:0::/root:/bin/bash

john --wordlist=/usr/share/wordlists/rockyou.txt --format=sha512crypt unshadowed.txt
Using default input encoding: UTF-8
Loaded 1 password hash (sha512crypt, crypt(3) $6$ [SHA512 128/128 AVX 2x])
Cost 1 (iteration count) is 5000 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
1234             (root)
1g 0:00:00:00 DONE (2021-05-06 05:56) 2.083g/s 2666p/s 2666c/s 2666C/s kucing..poohbear1
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

### Task 7

What is Joker's password?

```
john --single --format=raw-MD5 joker.txt
Using default input encoding: UTF-8
Loaded 1 password hash (Raw-MD5 [MD5 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
Warning: Only 2 candidates buffered for the current salt, minimum 12 needed for performance.
Warning: Only 9 candidates buffered for the current salt, minimum 12 needed for performance.
Warning: Only 5 candidates buffered for the current salt, minimum 12 needed for performance.
Jok3r            (Joker)
1g 0:00:00:00 DONE (2021-05-06 06:48) 100.0g/s 19600p/s 19600c/s 19600C/s j0ker..J0k3r
Use the "--show --format=Raw-MD5" options to display all of the cracked passwords reliably
Session completed
```

### Task 8

What do custom rules allow us to exploit?

```
password complexity predictability
```

What rule would we use to add all capital letters to the end of the word?

```
Az"[A-Z]"
```

What flag would we use to call a custom rule called "THMRules"

```
--rule=THMRules
```

### Task 9

What is the password for the secure.zip file?

```
zip2john crack_zip.zip > zip_hash.txt


ohn --wordlist=/usr/share/wordlists/rockyou.txt zip_hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (PKZIP [32/64])
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
pass123          (crack_zip.zip/zippy/flag.txt)
1g 0:00:00:00 DONE (2021-05-06 07:04) 100.0g/s 819200p/s 819200c/s 819200C/s 123456..whitetiger
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

What is the contents of the flag inside the zip file?

```
THM{w3ll_d0n3_h4sh_r0y4l}
```

### Task 10

What is the password for the secure.rar file?

```
rar2john rar_file.rar > rar_hash.txt

john --wordlist=/usr/share/wordlists/rockyou.txt rar_hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (RAR5 [PBKDF2-SHA256 128/128 AVX 4x])
Cost 1 (iteration count) is 32768 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
password         (rar_file.rar)
1g 0:00:00:00 DONE (2021-05-06 07:08) 9.090g/s 581.8p/s 581.8c/s 581.8C/s 123456..charlie
Use the "--show" option to display all of the cracked passwords reliably
Session completed
```

What is the contents of the flag inside the zip file?

```
THM{r4r_4rch1ve5_th15_t1m3}
```

### Task 11

What is the SSH private key password?

```
python /usr/share/john/ssh2john.py id_rsa > id_rsa_hash.txt

john --wordlist=/usr/share/wordlists/rockyou.txt id_rsa_hash.txt
Using default input encoding: UTF-8
Loaded 1 password hash (SSH [RSA/DSA/EC/OPENSSH (SSH private keys) 32/64])
Cost 1 (KDF/cipher [0=MD5/AES 1=MD5/3DES 2=Bcrypt/AES]) is 0 for all loaded hashes
Cost 2 (iteration count) is 1 for all loaded hashes
Will run 4 OpenMP threads
Note: This format may emit false positives, so it will keep trying even after
finding a possible candidate.
Press 'q' or Ctrl-C to abort, almost any other key for status
mango            (id_rsa)
Warning: Only 2 candidates left, minimum 4 needed for performance.
1g 0:00:00:05 DONE (2021-05-06 07:15) 0.1964g/s 2817Kp/s 2817Kc/s 2817KC/sa6_123..*7¡Vamos!
Session completed

```