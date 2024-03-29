# IntroToBurp - Web Exploitation
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/0c85a1e2-3807-4c5f-9b4b-ec6e25283048)

## Hints
- Try using burpsuite to intercept request to capture the flag.
- Try mangling the request, maybe their server-side code doesn't handle malformed requests very well.
## Solution
You are given a link to a website and told to mangle the inputs to the server in order to get the flag. 
The first step is to open up burp suite and intercept a login request. You can fill the fields with anything.
I then sent the request to `repeater` in order to test different adjustments.
<br><br>
> ![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/7c404c8d-ff97-4385-b193-8972045d6860)
- If you change `submit` to anything else it will redirect you to the next step. (Not the value in `submit` but the actual word.) 
<br><br><br>
> ![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/b3c896fc-d95c-42ff-bfb3-366de02e0213)
- Then you copy the same procedure except you change `otp` to something else.  

<br><br>
This will take you to a third page which has the flag.
