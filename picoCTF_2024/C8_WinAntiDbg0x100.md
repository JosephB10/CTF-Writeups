# WinAntiDbg0x100 - Anti-Debugger in Windows
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/ce7881a3-92f4-4d27-9d4e-e093d58ff2ef)
## Hints
- Hints will be displayed to the Debug console. Good luck!
## Solution
You are given a windows executable and told to bypass the `anti-debugger` checks to get the flag. 
<br><br>
I downloaded `windbg` to debug the program and when I was watching a tutorial on how to setup `windbg` they showed how to disable a debugging flag.
- Open the exectuable with `windbg`
- `eb $peb+0x2 0x0`
- And run to get the flag

<br>My windows debugging needs some work, since I know next to nothing about this topic. 
