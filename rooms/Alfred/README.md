# Alfred Jenkins Room 

## Task 1 

How many ports are open? (TCP only)

```
$ nmap -sC -sV -oN nmap/initial 10.10.58.211
Starting Nmap 7.91 ( https://nmap.org ) at 2021-09-06 08:00 EDT

Nmap scan report for 10.10.58.211
Host is up (0.034s latency).
Not shown: 997 filtered ports
PORT     STATE SERVICE            VERSION
80/tcp   open  http               Microsoft IIS httpd 7.5
| http-methods: 
|_  Potentially risky methods: TRACE
|_http-server-header: Microsoft-IIS/7.5
|_http-title: Site doesn't have a title (text/html).
3389/tcp open  ssl/ms-wbt-server?
| ssl-cert: Subject: commonName=alfred
| Not valid before: 2021-09-05T11:59:21
|_Not valid after:  2022-03-07T11:59:21
|_ssl-date: 2021-09-06T12:01:15+00:00; 0s from scanner time.
8080/tcp open  http               Jetty 9.4.z-SNAPSHOT
| http-robots.txt: 1 disallowed entry 
|_/
|_http-server-header: Jetty(9.4.z-SNAPSHOT)
|_http-title: Site doesn't have a title (text/html;charset=utf-8).
Service Info: OS: Windows; CPE: cpe:/o:microsoft:windows

Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
Nmap done: 1 IP address (1 host up) scanned in 17.58 seconds


```

ANSWER: 3

What is the username and password for the log in panel(in the format username:password)

ANSWER: admin:admin 

What is the user.txt flag?

ANSWER: 79007a09481963edf2e1321abd9ae2a0


## Task 2


