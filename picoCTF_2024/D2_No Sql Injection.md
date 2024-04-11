# No Sql Injection
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/35269323-0ad6-4cbf-ad13-92c5717806ea)
## Hints
- Not only SQL injection exist but also NoSQL injection exists.
- Make sure you look at everything the server is sending back
## Solution
You are given a link to a website login page and a directory of the source code for the website. 
<br>Based on the title and hint the key is to use a No SQL injection. 
<br><br>


![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/0c99bd6e-b0e7-4aea-a865-feb920cddb90)
<br><br><br>
Looking through the source code it became apparent that JSON objects were not properly sanitized and you can use operator injection.
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/edc5c97f-620a-4ad0-957c-ffa9c68b2ff0)
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/0dd1b267-6e08-4924-857e-02836c1b0cb7)
https://portswigger.net/web-security/nosql-injection
<br><br> 
You can do this in burp suite or just in the browser. (If you are using burp suite I ran into formatting issues that I'll talk about at the end.)
- Entering `{"$ne": null}` into both the username and password fields bypasses the login page
  - "This query returns all login credentials where both the username and password are not equal to invalid. As a result, you're logged into the application as the first user in the collection."(PortSwigger)
- Open the Developer Tools before you login and look at the Network Tab (I'm using Firefox)
- Then once you login, you can see the response to your `/api/login/` `POST` request


<br>![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/e9943a09-37a5-4acb-8bf7-5c00c9bcec89)
<br><br>
Expanding the response field shows you that the first person you logged in as was `Josh Iriya`.
And included in their information was a `Token` which contained a base64 string. 
<br><br>Decoding that string gave the flag.
<br><br>
## Formatting Note
I found this solution pretty quickly when I started looking into No Sql injections. 
However I ended up spending 3 days on this CTF because I didn't format JSON correctly inside of Burp Suite.
<br><br>
You need to backslash (`\`), out the double quotes inside of Burp Suite. 
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/dd4f7499-e4e7-4f92-b686-a445a1181f54)
<br><br>
