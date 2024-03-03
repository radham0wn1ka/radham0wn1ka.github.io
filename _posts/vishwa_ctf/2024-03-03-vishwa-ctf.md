---
layout: post
title:  "vishwa ctf"
date:   2024-02-19 09:29:20 +0700
categories: vishwa ctf
usemathjax: true
---

# crypto-valentines day
- it was said it used portable network graphics
- so we know that staring bits pattern of png
- with that we get the key 
```
The first eight bytes of a PNG file always contain the following (decimal) values:

   137 80 78 71 13 10 26 10
```
## receck
```
f = open("test.png", "rb").read()
key = [f[0], f[1], f[2], f[3], f[4], f[5], f[6], f[7]]
print("key is ",key)
```
### result
```
key is  [137, 80, 78, 71, 13, 10, 26, 10]
```
## encrypted way 
```
from PIL import Image
from itertools import cycle
def xor(a, b):
    return [i^j for i, j in zip(a, cycle(b))]
f = open("original.png", "rb").read()
key = [f[0], f[1], f[2], f[3], f[4], f[5], f[6], f[7]]
enc = bytearray(xor(f,key))
open('enc.txt', 'wb').write(enc)
```
### solve.py
```
from itertools import cycle
def xor(a, b):
    return [i^j for i, j in zip(a, cycle(b))]
enc_file=open("enc.txt","rb")
enc_data=enc_file.read()
print("size of enc_data is ",len(enc_data))
print("ecn data[:50]",enc_data[:50])
key = [137, 80, 78, 71, 13, 10, 26, 10]
dec_file=open("dec.png","wb")
dec_file.write(bytes(xor(enc_data,key)))
enc_file.close()
dec_file.close()
```
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/316432f8-5164-4e6b-b2fa-bd1568bef076)
VishwaCTF{h3ad3r5_f0r_w1nn3r5}


# web-trip to us
- on inspecitn we see
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/eadc9a73-88e4-49e3-af30-68dd15522647)
- that on clicking on click here we go to err.php
- once we go there and inspcect once agin
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/678ee06e-f46a-4bca-840e-ff766026c4be)
- we see the alt is
```
 alt="Change User agent to 'IITIAN'
```
- so we user burp suit
- so we change it and see we get 302
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/59a9b900-f297-4811-a029-dd8a1616b2ff)
- we follow redireciton<br/>
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/10e60297-f022-4323-a79d-3ee3ab5f3e40)
- we see a new endpoint
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/80fee9d6-8c63-423d-9b4c-abfe340188e5)
### try sql injection
- try admin' and abc as pass
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/4748e77b-3b5f-4c3d-b2fe-5194a2ff66d4)
- so there is a sql injection vulnerability
- admin" does not give any query err
- try admin'#
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/60af7c51-c0b5-4f3f-9d91-f5fd8ded0f5e)
<br/>
VishwaCTF{y0u_g0t_th3_7r1p_t0_u5}



## at last
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/27616f5c-9d52-4fa6-9f7f-88e5a4dbb298)
