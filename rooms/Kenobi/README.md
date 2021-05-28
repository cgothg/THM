# Notes for the room "Kenobi"

## Tasks 

### Task 1 

Scan the machine with nmap, how many ports are open?

```
7
```

### Task 2

Using this command specified in the task:

```
nmap -p 445 --script=smb-enum-shares.nse,smb-enum-users.nse 10.10.33.212
```

Using the nmap command above, how many shares have been found?

```
3
```