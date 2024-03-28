# Collaborative Development - git repo
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/6c19d797-c082-47c0-8bef-8a64cf1f1244)
## Hints
- `git branch -a` will let you see available branches
- How can file 'diffs' be brought to the main branch? Don't forget to `git config`!
- Merge conflicts can be tricky! Try a text editor like nano, emacs, or vim.
## Solution
You are given a git repo and from the description will need to merge multiple branches together. 
- `git branch -a` Shows you the names of the different branches
- `git merge [branchName]` Allows you to merge them together
- There are three branches and the first merge works without a problem

<br><br>
On the second merge I got this message.
<br><br>
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/0d3391d0-782a-433e-9d41-3acaa20ec9e1)
<br>
I used `git config --global user.email "you@example.com"` to set a fake email and get past this check.
<br><br><br><br>
Then you get a merge error. You need to open `flag.py` in a text editor and resolve the conflicts.
> ![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/df39b74b-c589-441c-9e1e-f79607804dcd)
> ![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/70c320bc-0b96-4553-966d-37721ee859db)
<br><br>
- Once you have fixed the merge error, you can finish the merge with...
- `git add flag.py` and `git commit -m "fixed merge error"`

Repeating this for the third merge, you don't really need to resolve the merge error again. You already have the flag.
