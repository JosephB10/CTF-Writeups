# Scan Surprise - QR Code
![image](https://github.com/JosephB10/CTF-Writeups/assets/105746932/2ff5e8f6-e963-4ce3-ad31-47d46328f4f7)
## Hints
- QR codes are a way of encoding data. While they're most known for storing URLs, they can store other things too.
- Mobile phones have included native QR code scanners in their cameras since version 8 (Oreo) and iOS 11
- If you don't have access to a phone, you can also use zbar-tools to convert an image to text
## Solution
You are given a `.png` file. Based on the description you just need to scan the QR code.
- On my kali linux the command to read QR codes is `zbarimg flag.png`
- And it spits out the flag
