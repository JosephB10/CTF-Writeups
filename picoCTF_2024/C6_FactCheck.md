# FactCheck - Reverse Engineering
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/bbe89e29-dbcb-4c1b-b7db-dd53b2ed10f5)
## Hints
- (None)
## Solution
You are given a binary and told to find the flag with it. 
<br>
Looking at the binary with ghidra you get the initial string `picoCTF{wELF_d0N3_mate_`, and then the rest of the flag is constructed from a complicated series of instructions.
<br><br>
Rather then try and follow what each part of the code does, I just used a debugger to get the completed flag at the end of the execution.
<br><br>
I normally would use `Radare2` as my debugger of choice but I was having some problems with it. My initial solve during the challenge week I was able to 
view the variable on the heap, but I think when the challenge was updated the completed flag was moved to the stack. And I was having trouble getting the proper ASCII readout from the stack with `r2.` 
<br><br>
However I was able to get the flag with `edb` debugger.

- `edb --run bin`
- Then I stepped through the program with `F8`
- And you could watch the flag being built in the stack

![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/e44bbcc3-1189-4e9a-9662-3b9fa821eca3)

<br><br>
I'm going to keep trying to setup `r2` in a way that lets me also see the flag being built. It's a little confusing that it didn't work.
