# Unfinished Attempts

There were two CTF's that I started working on but was unable to finish in time. 

## WinAntiDbgx200
I actually spent a decent amount of time working on this one, but I have almost no experience working with Windows Debuggers.  
<br><br>
I tried stepping through the program with `WINDBG` but was unable to figure out when it performed the anti-debugger checks. 
- Reading on discord after the event was over, I should've opened it in Ghidra

<br>Then I tried using `x64dbg` with the `scyllahide` plugin.
- Everytime I activated `scyllahide` the executable immediately exited
- Reading on discord I apparently needed to disable thread creation(?)

At least I have a small starting point for future learning. 


## SansAlpha
I only started this CTF exhausted after a long night working on `Trickster` and with a few hours left in the competition. 
<br><br>
Looking at writeups after the event was over, I was sort of on the right path. Trying to direct the output of `stderr` into a variable that I could then call parts of. 
<br><br>However I didn't know about wildcard command calling `/???/???` which might have prevented me from solving it. 
