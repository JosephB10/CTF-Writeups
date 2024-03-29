# Secret of the Polyglot - File Format
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/3ff9ad83-f3d7-4021-afb5-47b0515c3c85)
## Hints
- This problem can be solved by just opening the file in different ways
## Solution
We are given a file and told to open it in different ways to get the flag. 
<br>It's a `.pdf` file but if you run `file` the results show that it has `.png` image data.
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/17a5728e-bbd8-4ea2-881a-a02fad2a6ba0)
<br><br>
I used `cp` to make another version of the file with the extension `.png`.
<br>
Since I'm on kali I used `xdg-open` on both the `.pdf` and then the `.png` file to get both halves of the flag.
<br><br>
Note: You can also use `gio open` to open up a `.pdf` file.
