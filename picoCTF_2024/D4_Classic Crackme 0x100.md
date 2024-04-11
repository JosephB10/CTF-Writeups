# Classic Crackme 0x100
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/eb2f19ff-d0ca-4c6e-980f-b0fef94402ba)
## Hints
- Let the machine figure out the symbols!
## Solution
You are given an ELF and told to find the password in order to get the flag.
<br><br>
Opening it in ghidra it shows that there is a lot of different operations being done on your input, before it gets compared to the correct version.
- First thing I wanted to check was what the correct answer was, so I had something to work with
- Starting with `r2` , `aaa`, `pdf @main`, I set a breakpoint at the point just before the rdi, and rsa, were sent to `memcmp` to compare them
- `px @ rdi` conveniently showed both registers
  - The correct answer : `kgxmwpbpuqtorzapjhfmebmccvwycyvewpxiheifvnuqsrgexl`
  - and my result from the input `a` repeating : `addgdggjdggjgjjmdggjgjjmgjjmjmmpdggjgjjmgjjmjmmpgj`

<br>Just from looking at the code it clearly wanted a 50 char input to create the correct answer.
- My first thought was to get the decimal amount that each char strayed from the `a` value and then try and use that to reverse engineer the correct answer
- I did this pretty quickly, and didn't use a full 50 length string
  - But when I translated the correct answer with this method it resulted in a really ugly string of alphabetic characters and symbols
  - Assuming this wasn't the right answer I gave up and started down a rabbit hole
  - However this was the eventual solution that I ended up using
  - After spending an evening poring over the bitwise operations I realized that each char was independent of the ones before and after it, depending entirely on a strict algorithm to change their value
- I wasn't able to actually fully understand how the initial string was being manipulated into the final answer
- I recreated almost the whole program in python, but I'm guessing the real answer was that there was something going on with variable types, when they were being cast to chars 
- This is tough to see in ghidra because it had trouble figuring out which type to give the variables


<br>Back to my solution (This was almost certainly not the right solution)
- I took the correct string that was used as a check with `r2`
- Then I entered 50 `a` characters as the answer and took the result of that answer from the register (After it had been scrambled)
- A python script allowed me to extract the difference between each letter from the `aaaaa` string and the result
- Then I used the list of differences to reverse the correct string back into the password
- Entering that string gave the flag
