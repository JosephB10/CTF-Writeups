# binhexa - Binary Calculations
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/20c859aa-9d87-4278-8b23-02f4048afe59)
## Hints
None
## Solution
Told to connect to a listening port to answer binary calculations
<br>
Binary Number 1: 11001000
<br>
Binary Number 2: 00001001

- Question 1: `*` them together
	- 200 * 9 (Once converted to decimal)
	- 1800 which is `11100001000`
<br><br>
- Question 2: `+` them together
	- 200 + 9
	- 209 which is `11010001`
<br><br>
- Question 3: `>>` right bit shift, 1 bit, on Binary Number 2
	- 00001001 >> `00000100`
<br><br>
- Question 4: `<<` left bit shift, 1 bit, on Binary Number 1
	- 11001000 >> `110010000`
<br><br>
- Question 5: `&` them together 
	- `00001000`
<br><br>
- Question 6: `|` them together 
	- `11001001`
<br><br>
- Question 7: Convert the binary number from Question 6 to hexadecimal
	- `C9`
-  
<br><br>
After answering the final question the program gives you the flag.
<br>
https://www.geeksforgeeks.org/bitwise-operators-in-c-cpp/
