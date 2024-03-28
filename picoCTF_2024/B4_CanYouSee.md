# CanYouSee - Metadata
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/e9caf89e-839e-4112-9260-b1a0d7ea8f81)
## Hints
- How can you view the information about the picture?
- If something isn't in the expected form, maybe it deserves attention?
## Solution
You are given a `.jpg` file and told there is hidden data on it.
- `exiftool uknimage.jpg`
- There's a base64 string in the metadata
- Decoding it gives you the flag
