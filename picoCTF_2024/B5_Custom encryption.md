# Custom encryption - Cryptography
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/68b390cd-e6a2-46ae-9523-89a656e1b80b)
## Hints
- Understanding encryption algorithm to come up with decryption algorithm.
## Solution
### How the Encryption Works
This was a relatively tough one for only 100 points. You are given a `.py` file that was used to encrypt a string, and cipher file which is the result of the encryption. (It also includes 2 necessary variables.)
<br><br>The `.py` file has 3 important functions to understand.
1. `test`
> - Takes the flag inputted to the file and a key `trudeau`
> - Declares two values `p` and `g`
> - Generates 2 random values - `a` and `b` (These are provided in the cipher file)
> - It then passes all 4 of those variables to a `generator` function in different combinations to generate some sort of mathematical key
> - Following along with the math functions I got the `key` value `22`


2. `dynamic_xor_encrypt`
> - Takes the same input as `test`
> - Every character of the input flag starting from the last one is `xor`'d against a character from the repeating `trudeau`
>   - ie. `hello{myNameIsFlag}` reversed =  `}galFsIemaNym{olleh`
>   - Then each char is `xor`'d with it's matching char in `trudeautrudeautrudea`
> - Each number from this operation is then turned back into a char and recombined into a nonsense string

3. `encrypt`
> - Takes the encrypted string from `dynamic_xor_encrypt` and the `key` value(22) from `test`
> - For each char in the string it multiplies it's `ord` by 22 and then by the hard coded value `311`
> - This gives you a numerical value for each char in the original flag


### Decryption
I'll post my python script that decrypted it and explain each step.
- First you reverse the multiplication done in `encrypt` by dividing each cipher value by `22` and then by `311`
- Then create a repeating `trudeau` string the length of the cipher so you can perform `xor` operations with the right character
<br><br>
- Because `xor`'ing the result of a `xor` operation will reverse the process, we can just do that to get the original value
  - So we `xor` the char from trudeau with the reduced cipher value
<br><br>
- Then you just need to convert the decimal back into `ascii` and reverse it to get the flag

```
#The end result of the encryption
cipher = "61578, 109472, 437888, 6842, 0, 20526, 129998, 526834, 478940, 287364, 0, 567886, 143682, 34210, 465256, 0, 150524, 588412, 6842, 424204, 164208, 184734, 41052, 41052, 116314, 41052, 177892, 348942, 218944, 335258, 177892, 47894, 82104, 116314"
c_list = cipher.split(",")

#The given plaintext key
text_key = "trudeau"
key_length = len(text_key)
answer_rev = ""

#We can reverse it at the end
for i, ciph in enumerate(c_list):
    rev_multiply = int(int(ciph) / 22 / 311)    #Reverse the multiplication done on each character
    key_char = text_key[i % key_length]         #Repeat "trudeau" over and over again
    answer_rev += chr(ord(key_char) ^ int(rev_multiply))  #Reverse the xor operation by doing it again 
    
#Answer is backwards
print (answer_rev)

#Reverse the String
answer = answer_rev[::-1]
print (answer)


```
