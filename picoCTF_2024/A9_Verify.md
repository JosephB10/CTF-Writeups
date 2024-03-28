# Verify - Checksums
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/22c93298-d833-4ac0-ba70-3d4d899df07f)
## Hints
- Checksums let you tell if a file is complete and from the original distributor. If the hash doesn't match, it's a different file.
- You can create a SHA checksum of a file with sha256sum <file> or all files in a directory with sha256sum <directory>/*.
- Remember you can pipe the output of one command to another with |. Try practicing with the 'First Grep' challenge if you're stuck!
## Solution
You are given a directory with three things
1. `checksum.txt` This contains the correct checksum for the file you need to find
2. `decrypt.sh` This is a decryption script for the contents of the right file (Gives the flag if you decrypt the right file)
3. `files` A directory of files, 1 of the files has the encrypted flag as ascii

After getting the contents of `checksum.txt`, I used it to find the correct file by displaying all the checksums for the directory and then `grep`'ing to the right one.
- `sha256sum files/* | grep [contentsOf_checksum.txt]`
<br><br>
> ![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/8b9c4625-dbd8-4d75-ab6f-bf832d62fdea)

Now we know `files/451fd69b` is the file that we need to run `decrypt.sh` on.
However whether on purpose or by accident the code for `decrypt.sh` has the directory path of the `files` directory hard coded in. This would've worked for the person writing the code, but we need to change it.
<br><br>
- You can hard code the directory path for your machine
- OR you can switch it to a relative path `./`, like it should've been in the first place
- You need to do this for both checks  
> ![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/d3243f43-0b33-4667-8c56-113903fa2fe2)  
- Then providing `decrypt.sh` with the right file will give the flag
  - `decrypt.sh files/451fd69b`

<br><br>
I wasted some time on this challenge debugging `decrypt.sh`. This was because I hard coded the directory path as `~/mytmp/home/ctf-player/drop-in/...`. Unfortunately using `~` doesn't work in this context. I'm not totally sure why, but once this didn't work I assumed it was something other then the directory pathing and I went off down a rabbit hole. 


