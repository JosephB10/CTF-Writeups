# Unminify - Code Formatting 
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/99c3da67-72b6-47ac-b579-096af71ddcd2)
## Hints 
- Try CTRL+U / ⌘+U in your browser to view the page source. You can also add 'view-source:' before the URL, or try curl <URL> in your shell.
- Minification reduces the size of code, but does not change its functionality.
- What tools do developers use when working on a website? Many text editors and browsers include formatting.
## Solution
You are provided with a link to a website and told that the html has the flag.
- I went into the page source and copied the html
- Pasted it in a Visual Studio Code `.html` file
- If you right click on the code space there is an option to format the code


Then it's pretty easy to see the flag as a comment.
