# heap 1 - Binary Exploitation
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/a11b55b8-c72a-4af2-b633-500464455ac9)

## Hints
- How can you tell where safe_var starts?
## Solution
You are given a binary to practice on, the source code, and a remote instance to get the flag from. 
<br><br>
You need to cause a buffer overflow, but this time you have to change the programs variable to `pico`.
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/1fd57a45-f8cf-41f0-bec5-b80c0f1acbc9)

<br><br>
Using the binary you can see that the variable you need to change is 32 bytes away from the variable you control.
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/65584cb8-82fc-49dd-b573-9ca8b40dda79)
<br><br>
- `python3 -c 'print(("a"*32) + "pico")'`
  - Use 32 `a`'s to get to the variable and then `pico` to overwrite it with what we want  


- Copy paste that string into the `Write to buffer` option and then use the fourth option to print flag

<br>
Doing this on the remote instance will get you the flag.
