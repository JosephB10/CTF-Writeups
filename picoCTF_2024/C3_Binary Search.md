# Binary Search
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/271cc296-1b82-4a4c-8584-295d8e41f2e4)
## Hints
- Have you ever played hot or cold? Binary search is a bit like that.
- You have a very limited number of guesses. Try larger jumps between numbers!
- The program will randomly choose a new number each time you connect. You can always try again, but you should start your binary search over from the beginning - try around 500. Can you think of why?
## Solution
You are given the source code to practice on and a remote instance to get the flag from. 
<br>
It wouldn't be hard to write a simple program to solve this CTF automatically, but it's probably more time efficient to just do it manually.
<br><br>
You get 10 guesses to get a number between 1-1000 and it tells you if the number is higher or lower than your guess.
- Binary Search always splits the possible answers in half
1. 500 = higher
2. 750 = lower
3. 575 = higher
4. ... and so on until you get the right number and it gives the flag 
