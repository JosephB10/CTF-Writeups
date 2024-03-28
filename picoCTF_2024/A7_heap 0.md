# heap 0 - Binary Exploitation
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/0349ba18-8ebe-46e7-81aa-e0c57eead189)
## Hints
- What part of the heap do you have control over and how far is it from the safe_var?
## Solution
You are given a binary to test on, the `.c` source code, and a remote instance to actually get the flag from. 
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/47398e16-f0c7-40a0-ad6a-c8a9419677e4)
<br><br>
- Putting the hex addresses into a decimal converter shows that `pico` and `bico` are 32 bytes apart
- The option to "Write to buffer" allows us to write data directly to the heap
- And to get the flag all we need to do is change the value at the second address
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/e4704785-d768-4570-8f3e-8f2e4512c61e)
<br><br>
- Inputting more then 32 characters with the "Write to buffer" option will overwrite `bico`
- Then you can select option 4, to activate the win condition 
