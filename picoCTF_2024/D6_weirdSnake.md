# weirdSnake - Reverse Engineering
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/0cd093f0-754c-44b3-b427-58916ba871fe)
## Hints
- Download and try to reverse the python bytecode.
- https://docs.python.org/3/library/dis.html
## Solution
In this challenge you are given the Python bytecode disassembly of a program.
<br><br>You have to follow along with the bytecode's instructions reconstructing it in python in order to recreate the flag.
- I did this by alternating between chatgpt for definitions of what each line did, and writing a mirror python script so that I could compare it's disassembled script
- `import dis` and `dis.dis(main)` are how I was able to get a bytecode printout of my own


<br>The program initially declares an `input_list` of length 40 that's filled with integers (I used chatgpt to reformat this into a copyable list for my own code) 
- Then it creates a string key that's 5 characters long
- It runs list comprehension on this 5 char string to turn it into a list of integer values `(ord(char))`
- This is called `key_list`
- It then loops over this list extending it until it matches the length of the original `input_list`
- Finally it uses `zip` to turn the two lists into tuples, unpacks those tuples and does a `xor` operation on the two numbers, and creates a new list 
- Then it turns that list back into characters which is the flag

<br>This is the program I reconstructed
```
import dis

def myFunc(a):
    print a
    b,c=a
    return b ^ c

def main():
    input_list = [
        4, 54, 41, 0, 112, 32, 25, 49, 33, 3, 0, 0, 57, 32, 108, 23, 48, 4, 9, 70, 
        7, 110, 36, 8, 108, 7, 49, 10, 4, 86, 43, 102, 126, 92, 0, 16, 58, 41, 89, 
        78
    ]
         
    key_string = "t_Jo3"

    key_list = [ord(char) for char in key_string]

    while len(key_list) < len(input_list):
        key_list.extend(key_list)

    result = zip(input_list,key_list)
    resulty = [myFunc(tuples) for tuples in result]    
    result_text = ''.join(map(chr, resulty))

    print "\nresult_text: ",result_text

if __name__ == "__main__":
    dis.dis(myFunc)
    dis.dis(main)
    main()
```
<br><br>
My one hang up on this was that I didn't realize `key_string` was constructed in a devious way. Switching which side of the string each char was placed on.
<br><br>
Once I had `key_string` correctly formatted I ran the above code and it gave me the flag.
