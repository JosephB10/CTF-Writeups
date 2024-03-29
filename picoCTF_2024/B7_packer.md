# packer - Reverse Engineering 
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/81ccee83-57fd-4c8e-a62d-66770d9e16aa)
## Hints
What can we do to reduce the size of a binary after compiling it.
## Solution
We are given a binary that contains the flag. The task says that the binary has been compressed.
- I opened the binary in ghidra but couldn't find anything that way.
- `strings binary` showed that it had been packed by `upx`
- After looking this up, you can reverse the compression with `upx -d`

Re-opening the binary in ghidra, it now gets decompilied into something that makes sense.
<br>
Once ghidra finishes analyzing, the flag is visible.
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/e0c9bb49-15fd-4d37-b581-629f553fe3ef)

Decoding the string from hex will then give the flag.
