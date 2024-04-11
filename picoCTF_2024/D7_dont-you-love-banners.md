# dont-you-love-banners - Privilege Escalation
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/201168bd-69a5-44f1-aa62-942e78fb9bb0)
## Hints
- Do you know about symlinks?
- Maybe some small password cracking or guessing
## Solution

You are given an DNS to connect too. With a port number for a listening service and another port number that is "leaking information."
<br><br>Using `nc` on the leaking port gives you back the banner `SSH-2.0-OpenSSH_7.6p1 My_Passw@rd_@1234`.

<br><br>
Using `nc` on the service DNS it asks you questions...
- First question
  - `what is the password? `
  - `My_Passw@rd_@1234` We just got that
- Second question
  - `What is the top cyber security conference in the world?`
  - `DEFCON`  This was just a guess based on things I've heard
- Third question
  - `the first hacker ever was known for phreaking(making free phone calls), who was it?`
  - `John Draper` was what google came back with
 
<br><br>Now we are given a shell on the machine as user `player` with basic user permissions (1001).
- There is a `banner` file in the players directory
- In `/root` is the `flag.txt` (not readable) and a `script.py` which was called when you connected to the port
  - This is the script that asked the three questions
  - It was running as root on the port
- Inside the script it is made clear that it calls on the `banner` file to create a banner whenever it's executed


<br><br>If you combine this with the sym-links hint the solution is pretty obvious.
- `rm banner` Remove banner from the users directory
- `ln -s /root/flag.txt /home/player/banner` create a file called banner which is a symbolic link to the flag in root

<br><br>Now if you try and execute the script as `player`, (`python3 script.py`) it won't work because you don't have the necessary privilege to read the flag.txt.
- But if you disconnect and reconnect...
- Well then root is executing the script which reads the flag file through your symbolic link

<br><br>I've never used sym-links before and it's a neat little exploit that I'm glad I now know about. 
