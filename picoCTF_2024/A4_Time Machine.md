# Time Machine - git repo
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/42aae257-d57d-47d8-a48f-2dd32855cb3c)

## Hints
- The cat command will let you read a file, but that won't help you here!
- Read the chapter on Git from the picoPrimer https://primer.picoctf.org/#_git_version_control
- When committing a file with git, a message can (and should) be included.
## Solution
I'm thinking I came up with an unintended solution to the **Commitment Issues** problem since I repeat the exact same solution for this one... 
Though I didn't need to do the `git show` command since `git log` already showed the flag.
- `unzip challenge.zip`
- `git log`
- Profit
