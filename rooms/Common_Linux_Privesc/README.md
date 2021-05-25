# Notes for the room "Common Linux Privesc"


## Tasks

### Task 4


What is the target's hostname?

```
polobox
```

Look at the output of /etc/passwd how many "user[x]" are there on the system?

```
8
```

How many available shells are there on the system?

```
4
```

What is the name of the bash script that is set to run every 5 minutes by cron?

```
autoscript.sh
```

What critical file has had its permissions changed to allow some users to write to it?


```
/etc/passwd
```

### Task 5

What is the path of the file in user3's directory that stands out to you?


```
/home/user3/shell
```

### Task 6

Having read the information above, what direction privilege escalation is this attack?

```
vertical
```

Before we add our new user, we first need to create a compliant password hash to add! We do this by using the command: `"openssl passwd -1 -salt [salt] [password]"`

What is the hash created by using this command with the salt, "new" and the password "123"?

```
$1$[new]$QVSf2wqMC/UUOoXEaxKxR0
```

Great! Now we need to take this value, and create a new root user account. What would the /etc/passwd entry look like for a root user with the username "new" and the password hash we created before?

```
new:$1$new$p7ptkEKU1HnaHpRtzNizS1:0:0:root:/root:/bin/bash
```

### Task 7

Let's use the "sudo -l" command, what does this user require (or not require) to run vi as root?

```
NOPASSWD
```

### Task 8

What is the flag to specify a payload in msfvenom?

```
-p
```

What directory is the "autoscript.sh" under?

```
/home/user4/Desktop
```



