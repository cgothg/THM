# Notes for the room OWASP Top 10 (https://tryhackme.com/room/owasptop10). Part of the "Complete Beginner Path"

## Questions and answers:

### Task 5

What strange text file is in the website root directory?

- Just use the command `ls`

```
drpepper.txt
```

How many non-root/non-service/non-daemon users are there?

```
0
```

What user is this app running as?

- Check the user with `ps - ef`

```
www-data
```

What version of Ubuntu is running?

- Run the command `cat /etc/os-release`

```
18.04.4
```

Print out the MOTD.  What favorite beverage is shown?

- Run the command `cat /etc/update-motd.d/00-header`

```
dr. peper
```

### Task 7

What is the flag that you found in darren's account?

```
fe86079416a21a3c99937fea8874b667
```

What is the flag that you found in arthur's account?

```
d9ac0f7db4fda460ac3edeb75d75e16e
```

### Task 11

What is the name of the mentioned directory?

- Go to login page and view page source 

```
/assets
```

Navigate to the directory you found in question one. What file stands out as being likely to contain sensitive data?

```
webapp.db
```

Use the supporting material to access the sensitive data. What is the password hash of the admin user?

- `sq3lite webapp.db` --> `PRAGMA table_info(users);` --> `SELECT * FROM users;`

```
6eea9b7ef19179a06954edd0f6c05ceb
```

What is the admin's plaintext password?

```
qwertyuiop
```

Login as the admin. What is the flag?
```
THM{Yzc2YjdkMjE5N2VjMzNhOTE3NjdiMjdl}
```

# TO BE CONTINUED...