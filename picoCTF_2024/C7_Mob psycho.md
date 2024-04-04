# Mob psycho - Searching with `find`
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/5b7c28fd-0916-470a-bbaa-ba9d976f1f6b)
## Hints
- Did you know you can unzip APK files?
- Now you have the whole host of shell tools for searching these files.
## Solution

You are given an android APK, which seems to be a specific file system / os for android.

- Following along with the hints I looked online for how to unzip this kind of file
- `unzip file.apk -d hello`   Unzips it to a directory called hello  


<br>Then the next hint says to use shell commands to find the flag 
- `find /.../hello -type f -name *pico*` found nothing
- `find /.../hello -type f -name *flag*` found a .txt file called flag

Using `cat` on the file gave a hexadecimal string. I put the string into cyberchef and used the `from hex` option to get the flag.
