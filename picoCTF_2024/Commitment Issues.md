# Commitment Issues
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/36059ba9-ec3e-4847-b186-9357079d12d3)



## Hints
- Version control can help you recover files if you change or lose them!
- Read the chapter on Git from the picoPrimer here https://primer.picoctf.org/#_git_version_control
- You can 'checkout' commits to see the files inside them


## Solution

We are given a compressed cloned git repository.
- `unzip challenge.zip` to extract
  - We know it's a git repo because of the task description, but also because `ls -la` shows a `.git` file
<br><br>
- `git log` shows us the different commits that have been done to the repo
  - It also provides us with each commit's ID
<br><br>
- `git show 7d3aa557ff7ba7d116badaf5307761efb3622249` 
  - `7d3aa...` is the ID from the `git log` command
<br><br>
- This shows us the code that was committed
  - And in this case we got the flag


