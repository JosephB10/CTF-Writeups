# Web Decode - Hidden Information On A Website
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/758f50fe-2cd6-4829-9906-de7002da5ad9)
## Hints
- Use the web inspector on other files included by the web page.
- The flag may or may not be encoded
## Solution
You are given a link to a website. 
- Opening the "About" page shows the text `Try inspecting the page!! You might find it there`
- Right-Click + `View Page Source`
- There is a base64 encoded string `cGljb0NURnt3ZWJfc3VjYzNzc2Z1bGx5X2QzYzBkZWRfZjZmNmI3OGF9`
- Decoding it in cyberchef gives the flag
