---
title: "PUT Security Day Challs"
date: 2018-11-12T15:12:15+01:00
draft: false
---

### Intro

As promised, we are publishing our tasks from recent CTF hosted during PUT Security Day vol. 0!

### Stegano

##### Stegano seal [100] 

[file](https://ctf.pozsec.pl/files/9a55714049d387addda664d999db2e57/seal.png)

"You have been visited by a stegano seal. It brings you joy (and points)."

##### Art Gallery [150] 

[file](https://ctf.pozsec.pl/files/28b84102c686b61dacbf55879b8b51b6/Do_you_like_art.png)

"Do you like the art?"

##### Relativity [200]

[file](https://ctf.pozsec.pl/files/26d1752055310418f5cc874f8de17d44/Relativity.wav)

There's something weird about the recording we've received.

Once you got the message, wrap it with `PUT{` and `}`, and make it uppercase (e.g. if the message was "example", the flag would look like `PUT{EXAMPLE}`).

(Actually the challenge falls into stegano/crypto category) 

##### PNG wildcat

[file](https://ctf.pozsec.pl/files/d74e0231a9152a044bc52b90b2839136/wildcat.png)

I bet he holds some kind of a secret


### RE

TBA

### Misc

##### Sanity Check [5]

`HACK THE PLANET!` ofc :)

##### QR text [50]

[file](https://ctf.pozsec.pl/files/1e25491e1a18b5f2dddfb4dda44879cf/weird_file.txt)

What's wrong with that file?!

HINT: Try inverting things..

##### Galactiv Noise [150]

[file](https://ctf.pozsec.pl/files/e3bbb86ad5e5da504d348fb50d450b0d/moutains.wav)

We've never heard that... WTH?!

Probably you want to ask Scotie ;)

###### Msg from our intelligence

[file](https://ctf.pozsec.pl/files/4b0ac392c4fd9ab95389e1fb9c257e06/message_from_our_intelligence.7z)

We have received a message from one of our best agents.

Can you help us decipher it?

### Crypto

##### SingleByte [80]

[file](https://ctf.pozsec.pl/files/34c92d82be7b04176cec7718ca925a38/ciphertext)

Somewhere in the middle - there is a flag...

HINT: how about XOR?

##### SimpleCrypt [100]

[file](https://ctf.pozsec.pl/files/5646827822297221dd1aa5062a22f080/ciphertext.txt)

##### EzRSA [200]

```
n = 0xb51efc673cc8e95dd2b2a5c57fe17442ffe0e839545251d99f57d4f849847b999ab49d69727e3cdf8c46b0d58b2911077e72f5a6365f61ffe0fe32ecb73d6eaba83802192a91047da500382d0564735f614365bdf841c37a13e5636fb4d1358ca930b7143a2b0306954b1602124a19e25d0847251a3f6bae8d54cfe0e9842f3c63d58c3a275e98aad52a57e3058af22b3aaef24ad4808ce3a1252785002d06a62b5c1ef9466dce8954b9f1d912911b369a6c0ae64bdf6b2342fc1787a59cddc9414ce7ce26572579ea1e9600d8cb686f2f15784124f6eeb496893c5349127ccb2e42b838e8394de2acb2aaa4325a7ae732c8fe5d6b4d7d47ad6f8ef6799822c5

e = 3

d = 10158842775944441879845412522073645913593431921496039304017563009015613000152961953010735286029351465992156858265490011638069859459408299210172354146587934259469618944647452912521483719003264592154023983871077

```

What now?

#####  Back to the future [250]


Our agency not only uses bulletproof crypto, but also steals secrets from the future. Unfortunately we cannot decrypt the message. Can you help us?

https://goo.gl/tY13CE
