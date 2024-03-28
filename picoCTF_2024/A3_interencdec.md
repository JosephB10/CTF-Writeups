# interencdec - Decrypting Strings
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/be6de807-4544-4ba3-b5b3-d57ffb2ab777)

## Hints
- Engaging in various decoding processes is of utmost importance
## Solution
You are given an ascii text file with the string `YidkM0JxZGtwQlRYdHFhR3g2YUhsZmF6TnFlVGwzWVROclh6ZzVNR3N5TXpjNWZRPT0nCg==`. Based on the description multiple decoding steps will get you the flag. 
- I use cyberchef for these kinds of challenges but you could do it all in terminal
- Based on the upper and lowercase letters, numbers, and with the string ending in **"=="**, I assumed the first step was base64
<br><br>
- Base64 decode = `b'd3BqdkpBTXtqaGx6aHlfazNqeTl3YTNrXzg5MGsyMzc5fQ=='`
- The `b' '` indicated that it was a byte literal
- If you remove the byte literal and decode as base64 again you get
  - `wpjvJAM{jhlzhy_k3jy9wa3k_890k2379}`
<br><br>
- This looks like a caesar cipher in the "picoCTF{}" flag format
- I used a caesar cipher decoding website and provided it with "picoCTF" as a plaintext key to look for 
  - https://www.dcode.fr/vigenere-cipher
<br><br>
- and got the flag 
