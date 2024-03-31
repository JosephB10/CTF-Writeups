# endianness
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/bfa4ffee-e7ab-4b56-86e3-1ecbb96dc9de)
## Hints
- You might want to check the ASCII table to first find the hexadecimal representation of characters before finding the endianness.
- Read more about how endianness here https://levelup.gitconnected.com/little-endian-and-big-endian-74ab6441b2a7
## Solution
You are given a remote connection to a questionnaire and the source for the code.
<br><br>
The goal is to turn words into little and big endian. I was a little confused by what they meant by this. Were we supposed to adjust the letters of the word into 2 char blocks? 
- To figure out what they wanted I added a couple print statements to the source code and then compiled it
- After playing around with this it was clear that you...
  1. Convert the word into it's ascii hexadecimal representation
  2. Then you can convert the hex into little or big endian  

<br><br>
So `hello` becomes `68 65 6C 6C 6F`
Little Endian = `6F 6C 6C 65 68`
Big Endian = `68 65 6C 6C 6F`
<br><br>
Answer these correctly and you get the flag.
