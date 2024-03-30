# format string 1 - Binary Exploitation
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/0eb14bdf-92cb-4f8f-b403-2dae705b19d3)
## Hints
- https://lettieri.iet.unipi.it/hacking/format-strings.pdf
- Is this a 32-bit or 64-bit binary?
## Solution
You are given a compiled binary to test on, the source code, and a remote instance which has the flag.
<br><br>
This challenge involved exploiting format-strings, through incorrectly formatted `printf` statements in `C`. 
Essentially this allows you to perform memory reads and writes by entering a format symbol into the input. 
<br><br>
For this CTF we will be using `%lx` to read 8-bit stack lines because the binary is 64 bit. If it was 32 bit we'd use `%x` instead.
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/b5a77406-16fa-485f-b610-4b6119856d11)
<br><br>
Also the first 5 results of `%lx` will be registers.
<br>
So when the program asks for input, I provided it with `%lx.%lx.%lx...` repeating 200 times.
<br><br>
This gives back 8-bit hexadecimal values in memory. 
<br>
This then has to be sanitized to be made readable. This was the toughest part of the CTF for me.
<br><br>
I got help writing this python script which turns each hexadecimal value into decimal and then uses `pwntools` to pack it from 64 bit. 
<br><br>
```
import pwn
value = "402118.0.7f9932a6fa00.0...."
valist = value.split(".")

newlist = [print(pwn.p64(int(x,16)))for x in valist]

print (newlist)

```

This turns the raw memory output into readable strings. The flag was then visible.

