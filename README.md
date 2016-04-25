# PassCard

PassCard is a simple system to create strong passwords on the go, without the need of a smartphone or computer program.

## Overview
PassCard generates a key card you can carry around with you to create passwords whenever you need them. When you use PassCard to generate a card, you simply supply it with a passphrase of your choosing (which can be used to re-generate your card in the future), and PassCard will generate a printable card.

The card is formatted as follows:
```
a:m#c b:hjy c:qz3 d:U5X e:IlQ 
f:gOT g:t2! h:lP5 i:yxz j:aD! 
k:v33 l:V$O m:RpV n:@Z3 o:z_Y 
p:W$L q:E$h r:lZJ s:dwt t:Ut$ 
u:rpi v:3UE w:lWd x:mKB y:Ajo 
z:T2a 1:m2! 2:MRS 3:EU# 4:zaQ 
5:2IP 6:faY 7:p$1 8:fmk 9:YIz 
0:$GI
```

This grid of data corresponds to each letter of the english alphabet and numbers 0-9. To use this system you simply come up with a word you want to use as the 'short form' of your password and translate it into a longer string. For example, if you are creating a password for your banking site the short form password could be 'bank1', using PassCard that would be translated into 'hjym#c@Z3v33m2!'.

The intersting thing about using this system is that over time you will begin to remember the 3 character combinations that follow each letter or number, enabling you to use the system without even looking at the card. 

## Security and Implementation
The implementation of this system is fairly straight-forward and seems like it would be reasonably secure. **I am always looking for feedback that could make this application more secure.**

### How It Works:
* We start with a list of all printable ASCII characters from char 33 to 127, this is the pool of characters we can use to generate cards.
* The users PassCard generation pass phrase is split in two, each chunk is hashed, and those two hashed values are converted to hex and concatenated. This gives us a nice long psuedo-random string.
* This long string is broken into chunks of 2 characters, each chunk is converted to an integer mod 94 (length of our pool), those integers are then used to retrieve 3 characters at a time from our pool and assign them to a-z and 0-9 for the grid.

