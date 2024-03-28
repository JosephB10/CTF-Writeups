# format string 0 - Binary Exploitation
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/c767c708-e036-46b6-9b64-213c1b645065)
## Hints 
- This is an introduction of format string vulnerabilities. Look up "format specifiers" if you have never seen them before.
- Just try out the different options
## Solution
You are given a compiled binary to test on, the `.c` source code, and a remote instance to actually get the flag from. 
- Looking at the source code we can see that a segfault will print the flag
<br><br> ![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/de26e5a6-5889-448c-a89c-c169033de32d)
- Also you can see in that picture that `BUFSIZE` is 32 bytes
<br><br>![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/7de048a2-31cf-4787-bf44-0d1c5c763614)
- When the program calls for input with `scanf` it assigns that input to a char array of size `BUFSIZE`
<br><br>
- So entering any input that's more then 32 characters will cause a segfault and give you the flag



