# Blame Game - git repo
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/cdd6b579-5a5a-426c-9cf8-b7a5167dbc4a)
## Hints
- In collaborative projects, many users can make many changes. How can you see the changes within one file?
- Read the chapter on Git from the picoPrimer https://primer.picoctf.org/#_git_version_control
- You can use python3 <file>.py to try running the code, though you won't need to for this challenge.
## Solution
You are given a git repo. Looking at the commits with `git log` shows a huge list of useless commits. 
- Near the bottom was an entry
  - `optimize file size of prod code`
<br><br>
- and the author was the flag 
