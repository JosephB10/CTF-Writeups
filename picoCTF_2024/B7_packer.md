# packer - Reverse Engineering 
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/81ccee83-57fd-4c8e-a62d-66770d9e16aa)
## Hints
What can we do to reduce the size of a binary after compiling it.
## Solution
We are given a binary that contains the flag. The task says that the binary has been compressed.
<br><br>
- I opened the binary in ghidra but couldn't find anything that way.
- `strings binary` showed that it had been packed by `upx`
- After looking this up, you can reverse the compression with `upx -d`
<br><br>
