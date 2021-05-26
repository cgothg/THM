# Notes for the room "Linux PrivEsc"

## Tasks 

### Task 1

Run the "id" command. What is the result?

```
uid=1000(user) gid=1000(user) groups=1000(user),24(cdrom),25(floppy),29(audio),30(dip),44(video),46(plugdev)
```

### Task 3

What is the root user's password hash?

```
$6$Tb/euwmK$OXA.dwMeOAcopwBl68boTG5zi65wIHsc84OWAIye5VITLLtVlaXvRDJXET..it8r.jbrlpfZeMdwD3B0fGxJI0
```

What is the root user's password hash?

```
sha512crypt
```

What is the root user's password?

```
password123
```

### Task 5


Run the "id" command as the newroot user. What is the result?

```
uid=0(root) gid=0(root) groups=0(root)
```

### Task 6

Visit GTFOBins (https://gtfobins.github.io) and search for some of the program names. If the program is listed with "sudo" as a function, you can use it to elevate privileges, usually via an escape sequence.


How many programs is "user" allowed to run via sudo? 

```
11
```

One program on the list doesn't have a shell escape sequence on GTFOBins. Which is it?

```
apache2
```

### Task 9

What is the value of the PATH variable in /etc/crontab?

```
/home/user:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin
```

### Task 16

What is the full mysql command the user executed?

```
mysql -h somehost.local -uroot -ppassword123
```

### Task 17

What file did you find the root user's credentials in?   

```
/etc/openvpn/auth.txt
```
