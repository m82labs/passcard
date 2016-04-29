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

## Examples

### With a user supplied passphrase, for a-z and 0-9
```
$ ./passcard -p 'My big passphrase for passcard' -d

------------------------------
a:zqd b:yoi c:517 d:bx3 e:B6U
f:2pX g:Ch# h:BZ+ i:bP_ j:zMJ
k:?X= l:tsS m:Yg0 n:6W8 o:!MD
p:*Oc q:R!K r:J41 s:WZT t:7Gh
u:aL@ v:Pt$ w:d7_ x:3OR y:o$i
z:j8i 0:4TZ 1:DyL 2:4+u 3:tvM
4:5+N 5:YsJ 6:1*h 7:iJy 8:8Z5
9:iDI 
------------------------------

The following passphrase can be used to regenerate your card:
My big passphrase for passcard
```

### With no supplied passphrasem for a-z
```
$ ./passcard

------------------------------
a:r8O b:kC9 c:yoZ d:zg8 e:QH$
f:1Hs g:G** h:4IV i:uN_ j:TR0
k:7J0 l:AQr m:SIv n:qgX o:3fr
p:TXB q:jpf r:TQu s:@dM t:aaI
u:cYC v:szI w:MU1 x:7Au y:U$s
z:_Z- 
------------------------------

The following passphrase can be used to regenerate your card:
9455e50a-0db3-11e6-bc61-a088b4506b48
```

### Printable 3.5inx2.0in HTML Output
```
$ ./passcard -p 'My big passphrase for passcard' -d -o pcard.html

File generated.

The following passphrase can be used to regenerate your card:
My big passphrase for passcard
```

This produces the following:

![Image of PassCard](https://raw.githubusercontent.com/m82labs/passcard/master/PassCard.png)
