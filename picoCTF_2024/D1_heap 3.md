# heap 3
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/2fd37fc3-7a97-4a81-9586-084aa7c6554e)
## Hints
- Check out "use after free"
## Solution
We are given the source code for a binary, the binary compiled, and a remote instance to exploit and get the flag from.
The binary allows you to...
- Allocate your own object of whatever size you want
- See the x variable on the heap (which defaults to `bico`)
- Check if x variable is `pico` which gives the flag
- and free the `x` variable


![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/1929203b-80b8-44fe-aad8-510b0dc9799b)
<br><br>

Reading up on UAF vulnerabilities shows that...
- When you free up a chunk of memory, it gets put into something called `fastbins` or `UnsortedBins` with a last in first out system
- So if you then try and malloc the same size data structure it will give you the same memory that just got `free`'d
- The vulnerability in this program is that the `x` variable can be called later in the program, AFTER it had been `free`'d
- You can `free` `x`, reassign it to whatever we want, and then call it



Solution 
- `Free x` to free the 35 byte data structure that's holding `bico`
- `Allocate Object` 
	- use a 35 byte malloc so that it will select the recently `free`'d chunk of memory 
	- I used this string `aaaaaaaaaaaaaaaaaaaaaaaaaaaaaapico` (30 `a`'s and then `pico`) 
	- Since the data structure has 30 empty bytes before we reach the `bico` bytes
- Now you can check `Print x->flag` which shows that if the `x` variable is called it will point at the new memory
- `Check for Win` to get the flag 
