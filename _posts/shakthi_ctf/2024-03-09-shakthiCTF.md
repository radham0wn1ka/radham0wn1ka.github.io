---
layout: post
title:  "shakthi ctf"
date:   2024-03-9 09:29:20 +0700
categories: shakthi ctf
usemathjax: true
---
# profile
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/75167fd6-b177-4f2a-9a75-cd0d7f816ea5)
# scoreboard
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/8b0c7cb4-6cbd-4383-83e1-5d421a9752c8)
# sovled challenges
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/de63fab4-4242-4b5d-b22f-fd88ecba7066)
## web/delicious
- the description
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/63ece15d-a997-4162-880f-7f1d190b8157)
- on openign the site and seeing the network tab in developer console
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/3e9f8dd5-83f6-4628-a695-48c51d3ac474)
- as we see the trailing=  we can expect it is base64 encoded
- so we decode it 
- we see admin as 0
- there does not appear any protection mechanism against we changin its value
- so we change it to 1 (true)
- and agian encode it
 ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/05b59a96-d01e-4cad-aa0e-1976ce365a8c)
 - we send the request with this modifed cookie
 - we get the flag
  ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/4c7fa682-8842-4712-a3d4-035ab27fad5d)
  shaktictf{heyo_beginnerr_you_got_the_flag}
## web/find the flag
  - this is the description
  ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/77c2fa9a-64b5-461e-940d-5def64bd179e)
- the attaced code is 
```
import os
from flask import Flask, request, render_template
app = Flask(__name__)
@app.get('/')
def index():
    test = request.args.get('test', None)
    if test is None:
        return render_template('index.html')
    command = f"find {test}"
    try:
        output = os.popen(command).read()
    except Exception as e:
        output = f"Error: {str(e)}"
    return render_template('index.html', output=output)
if __name__ == '__main__':
    app.run(host='0.0.0.0', port=5000)
```
- so our request param test is goeing threoug the os.popen and the result is rendered
- this is the frontend
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/037ac7b7-e6f4-4857-9c00-fcafc6731448)

- os.popen https://www.tutorialspoint.com/python/os_popen.htm
- find cmd resource https://www.geeksforgeeks.org/find-command-in-linux-with-examples/
- find cmd usage
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/7341fe59-e430-4b96-b774-ef2b355f8e99)
- we try to test in cmd
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/e9594348-1367-4a0a-a086-4d392b7a4e1d)
- we try to test on the website
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/b450ab9f-c1f7-4d84-9ec3-9ed7a57aae7c)
- we try in cmd
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/38a28775-d0d6-438f-aea6-9ee6cc73ca4a)
- we try in website
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/ec1ea4ce-f899-450d-b3ab-618709fa7e1c)
- shaktictf{finally_you found_the_flag_hehehheh!}
## web/ultimate spider man
- description
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/fc060cb6-a19e-487f-850b-78d122640d3c)
- on the frontend
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/a6a4c660-0adb-4631-89df-c10807010354)
- on cliking buying product with id 1 of cost 1000
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/1548a2c6-1689-45f4-90b9-ab2135c8bd40)
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/1d8b7a35-9868-47e9-afb9-41ff3476dba1)

- we get a coolkie and on deconding
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/b80f4fd2-d8d2-4719-aa2b-61d115203e60)
- this is the checkout
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/17652ee6-2df8-4e22-a061-dc124c68648a)
- it is a get request with money
- on seding that get request we get payment successful
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/7c79ddde-0966-46b1-8f96-74b174432ab2)
- we change the sign to chekc
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/5bc17472-3e27-4328-95c2-1c410acd433e)
- so signature is verifed
- our balance is not changing after buying things
` even thoug the header and payload are same in both (buing,checkout) the signature is different(as of different secretes used maybe)`
#### try none on chekout
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/2b662a06-7239-4d0c-acf9-c4f3556d1ba5)
- eyJhbGciOiAiTm9uZSIsICJ0eXAiOiAiSldUIn0K.eyJhbW91bnQiOiA1MDAwfQo
- on complely removing the sign part we get a err
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/c7467c9a-c278-42cd-b7e2-389826673121)
- so we place a random char as sign
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/ce1ed63c-b684-4fe6-9232-fe6c067a7fa6)
- shaktictf{Y0u_4re_th3_ult1mat3_f4n}
## web/filters
- description
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/2cb909ac-241e-48f5-ade7-944397e6df75)
- frontend
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/a5e9c236-0d4d-4dbf-95f7-b1fda53e4624)
- provided code
```
 <?php
highlight_file(__FILE__);
$command = $_GET['command'] ?? '';
if($command === '') {
    die("Please provide a command\n");
}
function filter($command) {
    if(preg_match('/(`|\.|\$|\/|a|c|s|require|include)/i', $command)) {
        return false;
    }
    return true;
}
if(filter($command)) {
    eval($command);
    echo "Command executed";
} else {
    echo "Restricted characters have been used";
}
echo "\n";
?>
Please provide a command 
```
- we need to bypass the filter and read the flag.txt file
- we use 2 function here
- glob()-which returns the list of files which matched the given pattern
- so we do glob("fl")[0] ->which gives the file name
- we use this techniue as if need to read `flag.txt` but the letter a is filtered
- as can be seen in this https://www.w3schools.com/php/func_filesystem_file.asp
- `The file() reads a file into an array.`
- here itself we see 
```
 <?php
print_r(file("test.txt"));
?> 
```
- so we read the file test.txt and print it 
`https://ch2474162010.ch.eng.run/?command=print_r(file(glob('*fl*')[0]));`
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/f6983a82-4080-492e-a684-d7935688e5b6)

## rev/warmup
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/3b81471a-6a1c-4f65-a373-5def1ba098dc)
- on running the executable file 
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/109a92ae-27c1-4bb5-a1d6-6956bcf51756)
- by running the file command we see it is a elf executable
- we use ghidra run to disassemble the binary
- we go to the main funciton in ghidra
```
undefined8 main(undefined8 param_1,undefined8 param_2)
{
  int iVar1;
  size_t sVar2;
  long in_FS_OFFSET;
  char acStack_e8 [104];
  undefined8 uStack_80;
  undefined4 local_6c;
  undefined8 local_68;
  char *local_60;
  undefined8 local_58;
  undefined8 local_50;
  undefined8 local_48;
  undefined6 local_40;
  undefined2 uStack_3a;
  undefined6 uStack_38;
  undefined8 local_32;
  long local_20;
  local_20 = *(long *)(in_FS_OFFSET + 0x28);
  local_6c = 100;
  local_68 = 99;
  local_60 = acStack_e8;
  printf("Enter the flag: ",param_2,3);
  fgets(local_60,100,stdin);
  sVar2 = strcspn(local_60,"\n");
  local_60[sVar2] = '\0';
  reverseString(local_60);
  local_58 = 0x316e64333364217d;
  local_50 = 0x346c6c336e67335f;
  local_48 = 0x34726d55705f6368;
  local_40 = 0x31355f345f77;
  uStack_3a = 0x735f;
  uStack_38 = 0x74667b746831;
  local_32 = 0x7368616b746963;
  iVar1 = strcmp(local_60,(char *)&local_58);
  if (iVar1 == 0) {
    puts("\nYou got it!!");
  }
  else {
    puts("Oops, that\'s not the correct flag");
  }
  if (local_20 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    uStack_80 = 0x10137e;
    __stack_chk_fail();
  }
  return 0;
}
```
- user enterd string is in local60 `fgets(local_60,100,stdin);`
- then the string is reveresd ` reverseString(local_60);`
```
local_58 = 0x316e64333364217d;
  local_50 = 0x346c6c336e67335f;
  local_48 = 0x34726d55705f6368;
  local_40 = 0x31355f345f77;
  uStack_3a = 0x735f;
  uStack_38 = 0x74667b746831;
  local_32 = 0x7368616b746963;
```
- then at consecutive locaitons some hex data is stored
- then it is being compaed with user input string local_60 
```
iVar1 = strcmp(local_60,(char *)&local_58);
if (iVar1 == 0) {
    puts("\nYou got it!!");
  }
  else {
    puts("Oops, that\'s not the correct flag");
  }
```
- we just convert each part to ascii (by hex to asci converter) and we reassemble
```
  local_58 = 0x316e64333364217d;---1nd33d!}
  local_50 = 0x346c6c336e67335f;----4ll3ng3_
  local_48 = 0x34726d55705f6368;---4rmUp_ch
  local_40 = 0x31355f345f77;-----15_4_w
  uStack_3a = 0x735f;--------s_
  uStack_38 = 0x74667b746831;---tf{th1
  local_32 = 0x7368616b746963;---shaktic
  shaktictf{th1s_15_4_w4rmUp_ch4ll3ng3_1nd33d!}
```

## rev/cyber kingdom
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/539135d2-3729-4f28-b121-a987dd29df97)
### by disassembling in ghidra
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/0b898bb2-8646-47a9-af9a-13ae15915306)

```

undefined8 main(void)

{
  uint uVar1;
  long in_FS_OFFSET;
  int local_16c;
  int local_168;
  int local_164;
  int local_160;
  uint auStack_158 [36];
  int local_c8 [36];
  byte local_38 [40];
  long local_10;
  
  local_10 = *(long *)(in_FS_OFFSET + 0x28);
  srand(0x7b);
  for (local_16c = 0; local_16c < 0x23; local_16c = local_16c + 1) {
    uVar1 = rand();
    auStack_158[local_16c] = uVar1 & 0xf;
  }
  puts("\n\t||| Welcome to my Cyber Kingdom |||");
  puts("||| I have a quick task for you if you don\'t mind |||");
  puts("|| Find the correct flag for me and prove yourself! ||\n");
  printf("Please enter the flag: ");
  fgets((char *)local_38,0x24,stdin);
  for (local_168 = 0; local_168 < 0x23; local_168 = local_168 + 1) {
    local_38[local_168] = local_38[local_168] ^ (byte)auStack_158[local_168];
  }
  local_c8[0] = 0x72;
  local_c8[1] = 0x6d;
  local_c8[2] = 0x60;
  local_c8[3] = 0x65;
  local_c8[4] = 0x73;
  local_c8[5] = 0x62;
  local_c8[6] = 0x68;
  local_c8[7] = 0x7a;
  local_c8[8] = 0x6c;
  local_c8[9] = 0x7a;
  local_c8[10] = 0x77;
  local_c8[11] = 100;
  local_c8[12] = 0x31;
  local_c8[13] = 0x54;
  local_c8[14] = 0x77;
  local_c8[15] = 0x31;
  local_c8[16] = 0x6c;
  local_c8[17] = 99;
  local_c8[18] = 0x59;
  local_c8[19] = 0x67;
  local_c8[20] = 0x62;
  local_c8[21] = 0x31;
  local_c8[22] = 0x6c;
  local_c8[23] = 0x58;
  local_c8[24] = 0x31;
  local_c8[25] = 0x7d;
  local_c8[26] = 0x53;
  local_c8[27] = 0x7e;
  local_c8[28] = 0x3b;
  local_c8[29] = 0x62;
  local_c8[30] = 0x69;
  local_c8[31] = 0x30;
  local_c8[32] = 0x6c;
  local_c8[33] = 0x31;
  local_c8[34] = 0x72;
  local_164 = 0;
  for (local_160 = 0; local_160 < 0x23; local_160 = local_160 + 1) {
    if (local_c8[local_160] == (int)(char)local_38[local_160]) {
      local_164 = local_164 + 1;
    }
  }
  if (local_164 == 0x23) {
    puts("\nYou got it!!");
  }
  else {
    puts("\nNope, that\'s not the right path");
  }
  if (local_10 != *(long *)(in_FS_OFFSET + 0x28)) {
                    /* WARNING: Subroutine does not return */
    __stack_chk_fail();
  }
  return 0;
}

```
- flag length is 35
- ![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/da9cc6c9-48fb-45bd-8d4d-492739d65f7a)
- so here there is random number generation but it uses a seed so same random numbers will come all the time
- so austack contains the random number
- our user input is in local38
- it is xored with the austack
- the result is compared with the localc8
- our_input^the_fixed_array=localc8
- so to get the our_input which must be the flag
- our_input=the_fixed_array^localc8
- the fixed array can be found by
```
#include <stdio.h>
#include <stdlib.h>
int main() {
    srand(0x7b);
    int aray[35]={0};

    for (int i = 0; i < 35; i++) { 
        int x=rand() & 0xf;
        printf("%d,", x); 
    }
    printf("done");
    return 0;
}
```
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/00b633d2-45bb-4376-a45a-b09baf610097)
### solve.py
```
length=35
random_numbers=[1,5,1,14,7,11,11,14,10,1,0,12,1,11,4,5,5,7,6,1,14,5,11,7,0,14,12,12,15,12,13,0,1,14,15]
local_c8=['']*35
local_c8[0] = 0x72 
local_c8[1] = 0x6d 
local_c8[2] = 0x60 
local_c8[3] = 0x65 
local_c8[4] = 0x73 
local_c8[5] = 0x62 
local_c8[6] = 0x68 
local_c8[7] = 0x7a 
local_c8[8] = 0x6c 
local_c8[9] = 0x7a 
local_c8[10] = 0x77 
local_c8[11] = 100 
local_c8[12] = 0x31 
local_c8[13] = 0x54 
local_c8[14] = 0x77 
local_c8[15] = 0x31 
local_c8[16] = 0x6c 
local_c8[17] = 99 
local_c8[18] = 0x59 
local_c8[19] = 0x67 
local_c8[20] = 0x62 
local_c8[21] = 0x31 
local_c8[22] = 0x6c 
local_c8[23] = 0x58 
local_c8[24] = 0x31 
local_c8[25] = 0x7d 
local_c8[26] = 0x53 
local_c8[27] = 0x7e 
local_c8[28] = 0x3b 
local_c8[29] = 0x62 
local_c8[30] = 0x69 
local_c8[31] = 0x30 
local_c8[32] = 0x6c 
local_c8[33] = 0x31 
local_c8[34] = 0x72 
# print(local_c8)
for i in range(len(local_c8)):
    print(chr((local_c8[i])^random_numbers[i]),end='')
```
it is just doing the xor between c8 and the fixed random numbers
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/94b32bb4-47e5-468c-8e0d-39c8e5b48d3a)
shaktictf{wh0_s4id_fl4g_1s_r4nd0m?} 

## rev/operaion ultra
![image](https://github.com/m0wn1ka/ctf_writeups/assets/127676379/091e9ed6-5a59-49cd-8f8b-2089bc3e89cd)
### given ultra.py
```
import base64
def func_1(unk_str0, unk_str):
    flag_len = len(unk_str0)
    unk_str_len = len(unk_str)
    unk_str1 = bytearray(unk_str0, 'utf-8')
    for i in range(flag_len):
        unk_str1[i] = unk_str1[i] ^ ord(unk_str[i % unk_str_len])
    return unk_str1.decode('utf-8')
def func_2(unk_str0):
    flag_len = len(unk_str0)
    unk_str3 = [''] * flag_len
    j = 0
    for i in range(0, flag_len , 4):
        unk_str3[j] = unk_str0[i]
        unk_str3[j + 1] = unk_str0[i + 1]
        j += 2
    for i in range(2, flag_len, 4):
        unk_str3[j] = unk_str0[i]
        unk_str3[j + 1] = unk_str0[i + 1]
        j += 2
    return ''.join(unk_str3)
def main():
    unk_str = "U2hhZG93MjAyNA=="
    unk_str = base64.b64decode(unk_str.encode('ascii')).decode('ascii')
    unk_str0 = input("Enter the input: ")
    unk_str1 = func_1(unk_str0, unk_str)
    unk_str2 = func_2(unk_str1)
    unk_arr0 = [32, 0, 27, 30, 84, 79, 86, 22, 97, 100, 63, 95, 60, 34, 1, 71, 0, 15, 81, 68, 6, 4, 91, 40, 87, 0, 9, 59, 81, 83, 102, 21]
    for i in range(len(unk_str0)):
        if unk_arr0[i] != ord(unk_str2[i]):
            exit(0)
    print("\nCorrect Flag!\n")
if __name__ == "__main__":
    main()
```
### change variable name
```
import base64
def func_1(user_input, shadow_string):
    flag_len = len(user_input)
    fun1_result = bytearray(user_input, 'utf-8')
    for i in range(flag_len):
        fun1_result[i] = fun1_result[i] ^ ord(shadow_string[i % 10])
    return fun1_result.decode('utf-8')
def func_2(fun1_result):
    flag_len = len(fun1_result)
    func2_res_in_aray_from = [''] * flag_len
    j = 0
    for i in range(0, flag_len , 4):
        func2_res_in_aray_from[j] = fun1_result[i]
        func2_res_in_aray_from[j + 1] = fun1_result[i + 1]
        j += 2
    for i in range(2, flag_len, 4):
        func2_res_in_aray_from[j] = fun1_result[i]
        func2_res_in_aray_from[j + 1] = fun1_result[i + 1]
        j += 2
    return ''.join(func2_res_in_aray_from)
def main():
    shadow_string = 'Shadow2024'
    user_input = input("Enter the input: ")
    fun1_result = func_1(user_input, shadow_string)
    fun2_result = func_2(fun1_result)
    constants_array = [32, 0, 27, 30, 84, 79, 86, 22, 97, 100, 63, 95, 60, 34, 1, 71, 0, 15, 81, 68, 6, 4, 91, 40, 87, 0, 9, 59, 81, 83, 102, 21]
    for i in range(len(user_input)):
        if constants_array[i] != ord(fun2_result[i]):
            exit(0)
    print("\nCorrect Flag!\n")
if __name__ == "__main__":
    main()
```
### solve.py
```
# the final value that we need i.e after going thoguh fun1,fun2 with this it is checked against
final_need=[32, 0, 27, 30, 84, 79, 86, 22, 97, 100, 63, 95, 60, 34, 1, 71, 0, 15, 81, 68, 6, 4, 91, 40, 87, 0, 9, 59, 81, 83, 102, 21]
flag_len=len(final_need)
j=0
#create a array to store
new_array=[''] * flag_len
new_array_index=0
for i in range(0,flag_len,4):
    new_array[new_array_index]=i
    new_array_index+=1
    new_array[new_array_index]=i+1
    new_array_index+=1
    j+=2
for i in range(2, flag_len, 4):
        new_array[new_array_index]=i
        new_array_index+=1
        new_array[new_array_index]=i+1
        new_array_index+=1
        j += 2
## with these  2 for loops we make a new array which has the mapping of func2 indices to func1 indices 
function1_res_mapping=new_array
for i,j in zip(final_need,function1_res_mapping):
     print(i,":",j)
## now we try to get the result of func1
##func2 result                         :32  0 27 30
##corresponding mapping posion of func1:0   1 4   5
func1_result=[''] * 32
for i in range(len(function1_res_mapping)):
    func1_result[function1_res_mapping[i]]=final_need[i]
#now we got from final need to func1 result 
#now from func1 result to we need to get the user input
#func1 is just doing an xor operaiton 
#x=y^z
#x^z=>y
#func1 result=userinput^shadow  string
#so to get the userinput we just do the xor of shadow string and func1 result
#userinput=func1 result^shadow  string  
answer_array=[''] * 32
shadow_string = 'Shadow2024'
for i in range(32):
    answer_array[i] = chr(func1_result[i] ^ ord(shadow_string[i % 10]))
ans="".join(answer_array)
print("flag is ",ans)
#x=y^z
#x^z=>y
```
`flag is  shaktictf{Ul7r4_STe4l7h_SUcc3s5}`