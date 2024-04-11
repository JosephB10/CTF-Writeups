# endianness-v2
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/9cae8a91-5de2-4cb7-81a6-4a7862156f9c)

## Hints
- None
## Solution
You are given a file and told that it's bytes have a weird endianness.
<br>I opened the file with `xxd` to see the hexdump.
- Went to https://en.wikipedia.org/wiki/List_of_file_signatures to see all file signatures
- Then started searching (`ctrl-f`) through 2 byte combos to try and find what the file signature was


<br>The idea was that if I could find how the file signature had been shuffled, I could reverse it.
- `e0ff d8ff 464a 1000` was the file given
- `FFD8 FFE0 0010 4A46` is the signature for jpg files

<br>Since the actual signature is a little endian version of the file given, I used `xxd`'s `-e` tag to get a little endian dump of the file.
- The signature now showed correct so I just needed to save the changes
	- `xxd -e challengefile > fixed.txt`
	- `xxd -r fixed.txt fixed.jpg` (The -r tag will save the changes to your binary)

<br>Then I opened the `.jpg` file with `xdg-open`(kali) to get the flag
